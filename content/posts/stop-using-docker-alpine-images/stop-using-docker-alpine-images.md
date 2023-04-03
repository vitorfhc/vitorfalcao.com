---
title: "Stop using Alpine Docker images"
date: 2022-04-27T10:00:00-03:00
---

Everybody loves Alpine images because they are light and have a smaller attack surface, but maybe they are not the best option anymore. It's time to talk again about distroless images.

---

![](/001/docker_alpine_post_01.png "")

At SumUp, we use Kubernetes with Docker images a lot, so we are always looking for the best options when it comes to base images. Distroless images are not something new, but for some reason, I don't feel they've been adopted as much as they should.

## What is a distroless image?

D'abord, I have to say this isn't something new, and I mean it. It has been around for years, and you can check it in [GoogleContainerTools/distroless](https://github.com/GoogleContainerTools/distroless).

> “Distroless” images contain only your application and its runtime dependencies. They do not contain package managers, shells or any other programs you would expect to find in a standard Linux distribution.

This is enough to understand that your container won't have anything but what you are using.

## Why should I use them?

Nowadays everybody has a CI and CD pipeline, but sometimes it takes ages to build, push and pull images. Distroless images are lighter, which means faster pulling and pushing.

Distroless images won't necessarily make your build step faster, but they are going to improve pulling and pushing time. Docker provides a [super minimal](https://hub.docker.com/_/scratch) image that won't create extra layers when you use it as your image's base. Fewer layers are equal to faster downloads and uploads.

Faster pipelines mean faster feedback to developers and fewer CI minutes spent, which is important when you are using a tool like [Actions](https://github.com/features/actions).

Security is also an important matter because you should try to decrease as much as you can your attack surface. You shouldn't have tools like sudo or ping in your container if you are not going to use them.

> If your code is vulnerable, you are less susceptible to an RCE that leads to a shell, but the RCE is still happening.
> - Erick Durán

Tools that help a malicious actor to gather more pieces of information or perform privilege escalations should always be avoided. You should take a look at [erickduran/docker-distroless-poc](https://github.com/erickduran/docker-distroless-poc) README.

## When you shouldn't use distroless images

Quite easy to say when to use distroless images, but when you shouldn't use them?

If you want to debug your application inside the container you could profit from a shell and some other installed tools, but distroless doesn't have any of that. The obvious answer is to use normal images for development and keep distroless to production.

Using different images in the development moves the developers away from the real production environment, which is not ideal, but creating testing steps in your CI pipeline that uses the same environment as in production should cover this issue. Be careful with this trade-off.

## What about an example?

The repository [GoogleContainerTools/distroless](https://github.com/GoogleContainerTools/distroless#examples-with-docker) has an example of how to make a distroless image for a Golang tool.

![](/001/example.png "")

This is a simple and easy example, mainly because Golang resulting binaries don't have runtime dependencies by default.

Instead, let's suppose we need to create a distroless image to use ping binary because we will be using it in one of our services to check if a host is up. This means we need to find all runtime dependencies and [this is not an easy task](https://unrealcontainers.com/blog/identifying-application-runtime-dependencies/), but I'll keep it as simple as possible.

![](/001/example_02.png "")

I ran the ldd command in Ubuntu and it shows us its dependencies, so I developed the following Dockerfile. Also, note that not every runtime dependency was in the ldd command output and I had to use other methods to discover them.

![](/001/example_03.png "")

Yet, this is not the smartest solution. The Dockerfile above creates an image with 5.44MB and we could improve it by using Alpine instead of Ubuntu. If you run the same ldd command but inside an Alpine environment you also have fewer and lighter dependencies.

![](/001/example_04.png "")

It works well and **uses only 1.43MB**, which is **around 74% less space** than the Alpine image and the image we have built using Ubuntu in the first stage.

## Conclusion

The title says you should stop using Alpine, but I think I showed you that this is just a matter of doing the right choice for the right occasion. Also, combining Alpine and [scratch](https://hub.docker.com/_/scratch) creates amazing distroless images.

The problem is that building distroless images for your applications is still quite manual and not as fun as you wish. Since it requires greater efforts from developers it's usually left behind in favour of the famous Alpine images.

I think the idea is to use distroless images in production environments and while performing manual and automated tests. You don't want to make it more stressful for developers to debug applications.

I hope the community gives the deserved attention distroless images should have and this causes more improvements, like automating their creation as much as we can.