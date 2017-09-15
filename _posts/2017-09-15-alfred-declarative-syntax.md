---
layout: blog
categories: Jenkins
---
### 简介
相比 Groovy 语法，Declarative 更简单易用。
> As it is a fully featured programming environment, Scripted Pipeline offers a tremendous amount of flexibility and extensibility to Jenkins users. The Groovy learning-curve isn’t typically desirable for all members of a given team, so Declarative Pipeline was created to offer a simpler and more opinionated syntax for authoring Jenkins Pipeline.

#### Sections
- [agent](https://jenkins.io/doc/book/pipeline/syntax/#agent){:target='_blank'} <sup><b>required</b></sup>
```groovy
pipeline {
    // 能用的 Agents 都可以用
    agent any
    // 在 top-level 不启用，但必须在 stage 中指定
    agent none
    // Agents 标签，一个标签可能包含多个 Agent
    agent {
        label 'agents label name'
    }
    // 指定具体的 Agent
    agent {
        node {
            label 'agent name'
        }
    }
    // docker
    agent {
        docker {
            image 'maven:3-alpine'
            label 'my-defined-label'
            args  '-v /tmp:/tmp'
        }
    }
    // dockerfile
    agent {
        // dockerfile 和当前 Jenkinsfile 在同一目录
        dockerfile true
        // dockerfile 在其他目录
        dockerfile {
            dir 'someSubDir'
            // 额外参数
            additionalBuildArgs '--build-arg foo=bar'
        }
    }
}
```
- [post](https://jenkins.io/doc/book/pipeline/syntax/#post){:target='_blank'}
```groovy
pipeline {
    // top-level 或 stage
    post {
        // 不管完成状态是成功还是失败，始终会执行
        always { }
        // 和前一个 Job 状态比较，如果不一样就执行
        changed { }
        failure { }
        success { }
        // 黄色图标那种，一般是因为测试失败，或者代码不符合规范
        unstable { }
        aborted { }
    }
}
```
- [stages](https://jenkins.io/doc/book/pipeline/syntax/#stages){:target='_blank'} <sup><b>required</b></sup>
- [steps](https://jenkins.io/doc/book/pipeline/syntax/#steps){:target='_blank'} <sup><b>required</b></sup>
```groovy
// 层级结构
// pipeline > stages > stage > steps
pipeline {
    stages {
        stage('Build') {
            steps {

            }
        }
    }
}
```

#### Directives
- environment
- options
- parameters
- triggers
- stage
- tools
- when

#### Steps
- script