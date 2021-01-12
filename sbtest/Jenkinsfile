#!/usr/bin/env groovy

node {
    checkout scm

    docker.withRegistry('http://cargo.caicloudprivatetest.com', '9306f204-a839-420f-bb3f-74864299a335') {

        stage 'Build'

        def gradle = docker.image('cargo.caicloudprivatetest.com/caicloud/centos7jdk1.8gradle4.4.1')
        gradle.pull()
        gradle.inside('--user root --mount type=bind,src=/var/lib/jenkins/.gradle,dst=/root/.gradle') {
            git 'https://github.com/liuyangc3/sbtest.git'
            sh 'gradle bootRepackage'
            sh 'mv build/libs/app.jar ./app.jar'
        }

        // maven
        // def maven = docker.image('cargo.caicloudprivatetest.com/caicloud/centos7jdk1.8maven')
        // maven.pull()
        // maven.inside('--user root --mount type=bind,src=/var/lib/jenkins/.m2,dst=/root/.m2') {
        //    git 'https://github.com/liuyangc3/sbtest.git'
        //    writeFile file: 'settings.xml', text: '<settings><localRepository>/.m2</localRepository></settings>'
        //    sh 'mvn -B -s settings.xml clean bootRepackage'
        //}
    }

    stage 'Bake image'
    // pass gradle "." to this image, make sure
    // that Dockerfile and app.jar in  PATH "."
    def img = docker.build("cargo.caicloudprivatetest.com/caicloud/jenkins_jar", ".")
    img.push()
}

// Docker Pipeline Plugink doc
// https://go.cloudbees.com/docs/cloudbees-documentation/cje-user-guide/index.html#docker-workflow

// pipeline syntax
// https://jenkins.io/doc/book/pipeline/syntax/
