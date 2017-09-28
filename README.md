# Testing the ARG parameter in dockerfiles

References: https://docs.docker.com/engine/reference/builder/#arg

Within a dockerfile the ARG option is the only method to paramertize the FROM command, which led to this testing.

The ARG parameter is used via the `--build-arg arg=value` syntax on the docker build command line. 

With a dockerfile like:

ARG image
FROM ${image}
EXPOSE 80

The following command line:

`$ docker build --build-arg image=alpine -t img .`

Will result in a `img` image derived from `alpine:latest`.

ARG statements can also be used to parameterize other statements in the dockerfile. To use an ARG with other statements it must be declared after the FROM statement.

With a dockerfile like:

ARG image
FROM ${image}
EXPOSE 80
ARG tag
COPY ${tag}.txt \.

The following command line:

`$ docker build --build-arg tag=foo --build-arg image=alpine -t img .`

Will result in a `img` image derived from `alpine:latest`, with a `foo.txt` file copied into the root of the image.
