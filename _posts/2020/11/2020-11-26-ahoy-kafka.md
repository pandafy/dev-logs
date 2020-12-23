---
title: Ahoy Kafka!
published: true
---

It was decided that we will get our hands dirty with Kafka and BentoML today.
Instead of skipping parts of the documentation, I went through the getting
started doc line by line.

Initially, I was not able to make the getting started code work locally on my
system. Then I went to the example Python notebook and read their code. It
occurred to me that I did not create different modules properly. I fixed it
and it worked like a charm.

With a sample BentoML application at our disposal, we started exploring the
other aspect of the issue, i.e. Kafka. Instead of installing Kafka directly
on our machines, we thought it would be better to get a docker image to spin up Kafka.

To our surprise, there was no official Docker image available for Kafka.
We found some tutorials which referenced docker images of Kafka but it was not
available on Docker Hub anymore. Probably, the tutorials were old and forgotten.

After a couple of web searches, we found an up-to-date
[docker image for Kafka maintained by Bitnami](https://github.com/bitnami/bitnami-docker-kafka).
We had a concern that using an unofficial Docker image may hurt our
implementation. Later, we ruled out this concern, by assuming that anyone who
is planning to use our implementation would already have a decent knowledge of
Kafka and could spin up a Kafka server on their own.

Bitnami’s docker image was well documented but poorly organized. Since we were
impatient trying to get it working, we never went through the whole
documentation. As a consequence, it was not working as expected. We never
configured it properly to get it working as expected. After lots of hits and
tries, we finally were able to get it working.

We settled on using the [kafka-python library](https://github.com/dpkp/kafka-python).
Initially, we had troubles connecting the client to the Kafka server but it
turned out, we had not configured the environment variables for Kafka’s docker
image. Yes, again.

After setting appropriate environment variables, we were able to create a
connection with the python client. Yet, the message we are creating from the
Kafka producer is not getting consumer by Kafka consumer.

We will need to give this another try this tomorrow.

-----------------

### In other news

It was a busy day today. There were many things on my todos.
I had to attend a meeting with my minor project’s mentor which went as planned.
She was asked to make changes. I had to also participate in demos of the MLH
Fellowship Township Mid-way Hackathon project. The project demo was smooth and
luckily it worked fine.

Today marks exactly one year since my first contribution to OpenWISP. I feel lucky to be part of this community.
