all: spark zeppelin
push: push-spark push-zeppelin
.PHONY: push push-spark push-zeppelin spark zeppelin zeppelin-build

# To bump the Spark version, bump the spark_ver in Dockerfile, bump
# this tag and reset to v1. You should also double check the native
# Hadoop libs at that point (we grab the 2.6.1 libs, which are
# appropriate for 1.5.2-with-2.6). Note that you'll need to re-test
# Zeppelin (and it may not have caught up to newest Spark).
SPARK_TAG = 1.5.2_v1

ZEPPELIN_TAG = 0.7.1

DOCKER_REGISTRY = sz-pg-oam-docker-hub-001.tendcloud.com/library

spark:
	docker build -t $(DOCKER_REGISTRY)/spark:$(SPARK_TAG) .

zeppelin:
	docker build -t $(DOCKER_REGISTRY)/zeppelin:$(ZEPPELIN_TAG) zeppelin

push-spark: spark
	docker push $(DOCKER_REGISTRY)/spark:$(SPARK_TAG)

push-zeppelin: zeppelin
	docker push $(DOCKER_REGISTRY)/zeppelin:$(ZEPPELIN_TAG)

clean:
	docker rmi $(DOCKER_REGISTRY)/spark:$(SPARK_TAG) || :
	docker rmi $(DOCKER_REGISTRY)/spark || :

	docker rmi $(DOCKER_REGISTRY)/zeppelin:$(ZEPPELIN_TAG) || :
	docker rmi $(DOCKER_REGISTRY)/zeppelin || :
