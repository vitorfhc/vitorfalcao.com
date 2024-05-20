---
title: "Simple Bugs 0x02: Overwritting Uploaded Files"
date: 2023-04-06T12:00:00-03:00
cover:
    image: /trojan_horse.png
---

File upload bugs are not as common as before, but they're still out there. They can provide all levels of priority, from informational to critical.

---

# Introduction

A forum allows you to create a profile and upload a picture. A simple and ordinary feature.

Even though it uses legacy technology such as PHP, it is as hardened as possible. When this is the case, you need to go beyond the standard techniques, but this doesn't mean they are complex. Maybe, you need extra creativity.

# The hacking process

I tried several techniques, but I failed in all of them. I like to start gradually testing what I find on [HackTricks](https://book.hacktricks.xyz/pentesting-web/file-upload), increasing complexity. Searching for disclosed reports on the same bug type is also always reasonable. After failing multiple times, I realized I had missed a minor detail.

## File upload

When I uploaded the file, it was sent to an S3 bucket on AWS. It was served on the following path `/profile_pics/{username}.png`. This caught my attention because I can control the username, even though the application doesn't let me change it. It's a unique attribute for each user that must be chosen on registration.

![](/d01.jpg)

The most exciting part, which took me several minutes to see, is that it was making a transformation on my username. The `UserA` became `usera` on the file path.

At first, I thought the username validation was case-sensitive. If it was, I'd be able to register userA even though UserA exists. Then, I'd upload the picture as userA and it'd overwrite UserA's file. Unfortunately, it was case-insensitive. See the image below to understand what I wanted to achieve.

![](/d02.jpg)

## Username normalization

A few months ago, I read an excellent post about [mysterious bugs by 0xacb](https://0xacb.com/2022/11/21/recollapse/). I decided to try some normalization bugs, and [his tool](https://github.com/0xacb/recollapse) makes very easy to generate payloads. The hypothesis is that it would let me create one of the following usernames.

```text
UserÀ
UseŕA
UsèrA
UśerA
ÙserA
```

It did let me create the username `UseŕA`. The second hypothesis is that when I upload a picture using this user, it will go to `/profile_pics/useŕa`. Once more, I was right.

I decided to change one of the letters I knew would be transformed, which is an uppercase one. So I created even another user, now using `ÙserA` as its username. The expected and correct output would be `/profile_pics/ùsera`. But this time, it saved the file as `/profile_pics/usera`. We got our bug.

## Final test

As the final test, I had two users: `UserA` and `ÙserA`. I uploaded a dog photo as the profile picture for `UserA`. Then, I uploaded a cat image to the `ÙserA` profile page. User `UserA`'s profile picture was overwritten, and it was now a cat.

We confirmed it. We need to report the bug now.

# Why did it happen?

In this series of posts, I always try to explain why the bug happens. It helps to evolve the developer's mindset, which allows for finding more bugs. But, this time, I am still determining the root cause.

At first, I thought Linux wouldn't accept the `ù` letter in the file name. I ran the command `touch ùsera`, and it worked. The hypothesis was wrong.

I will investigate further and update this post.

# Conclusion

My thoughts weren't straightforward as they are put in this post. It took me hours, and I tried several other things before finding this.

I always study by reading blog posts and papers and watching conferences. This is what made me read the [0xabc](https://0xacb.com) post, which was helpful. It's part of my routine, and you should try it too.
