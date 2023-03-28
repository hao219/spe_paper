# 系统是在开源平台openwhisk上实现的
# 直接下载原始的开源平台代码，应用所做的代码改动即可

# 下载代码
git clone https://github.com/apache/openwhisk.git
cd openwhisk

# 恢复到代码修改时使用的版本
git checkout f3f62df748f78a33fae0dadb575b677e5acc6b1d
# 应用修改
git apply code.diff

# 编译controller
./gradlew :core:controller:distDocker -PdockerImagePrefix=${DOCKER_IMAGE_PREFIX} -PdockerImageTag=${DOCKER_IMAGE_TAG}
# 编译invoker
./gradlew :core:invoker:distDocker -PdockerImagePrefix=${DOCKER_IMAGE_PREFIX} -PdockerImageTag=${DOCKER_IMAGE_TAG}

# 推送docker镜像 docker push xxx
# 然后部署openwhisk时使用推送的docker镜像即可