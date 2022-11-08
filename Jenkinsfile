pipeline {
  agent {
    node {
      label 'maven'
    }

  }
  stages {
    stage('拉取代码') {
      agent none
      steps {
        container('maven') {
          git(credentialsId: 'git-id', url: 'https://github.com/yang354/cloud-admin.git', branch: 'master', changelog: true, poll: false)
          sh 'ls'
        }

      }
    }

    stage('项目编译') {
      agent none
      steps {
        container('maven') {
          sh 'ls'
          sh 'mvn clean package -Dmaven.test.skip=true'
        }

      }
    }

    stage('default-2') {
      parallel {
        stage('构建rouyi-auth镜像') {
          agent none
          steps {
            container('maven') {
              sh 'ls ruoyi-auth/'
              sh 'docker build -t ruoyi-auth:v1.0 -f ruoyi-auth/Dockerfile ruoyi-auth/'
            }

          }
        }

        stage('构建ruoyi-gateway镜像') {
          agent none
          steps {
            container('maven') {
              sh 'ls ruoyi-gateway/'
              sh 'docker build -t ruoyi-gateway:v1.0 -f ruoyi-gateway/Dockerfile ruoyi-gateway/'
            }

          }
        }

        stage('构建ruoyi-file镜像') {
          agent none
          steps {
            container('maven') {
              sh 'ls ruoyi-modules/ruoyi-file/'
              sh '''docker build -t ruoyi-file:v1.0 -f ruoyi-modules/ruoyi-file/Dockerfile ruoyi-modules/ruoyi-file/
'''
            }

          }
        }

        stage('构建ruoyi-system镜像') {
          agent none
          steps {
            container('maven') {
              sh 'ls ruoyi-modules/ruoyi-system/'
              sh 'docker build -t ruoyi-system:v1.0 -f ruoyi-modules/ruoyi-system/Dockerfile ruoyi-modules/ruoyi-system/'
            }

          }
        }

        stage('构建ruoyi-monitor镜像') {
          agent none
          steps {
            container('maven') {
              sh 'ls ruoyi-visual/ruoyi-monitor/'
              sh 'docker build -t ruoyi-monitor:v1.0 -f ruoyi-visual/ruoyi-monitor/Dockerfile ruoyi-visual/ruoyi-monitor/'
            }

          }
        }

        stage('构建ruoyi-job镜像') {
          agent none
          steps {
            container('maven') {
              sh 'ls ruoyi-modules/ruoyi-job/'
              sh '''docker build -t ruoyi-job:v1.0 -f ruoyi-modules/ruoyi-job/Dockerfile ruoyi-modules/ruoyi-job/
'''
            }

          }
        }

      }
    }

    stage('default-3') {
      parallel {
        stage('推送ruoyi-auth镜像') {
          agent none
          steps {
            container('maven') {
              withCredentials([usernamePassword(credentialsId : 'aliyun-docker-registry' ,passwordVariable : 'DOCKER_PWD_VAR' ,usernameVariable : 'DOCKER_USER_VAR' ,)]) {
                sh 'echo "$DOCKER_PWD_VAR" | docker login $REGISTRY -u "$DOCKER_USER_VAR" --password-stdin'
                sh 'docker tag ruoyi-auth:v1.0 $REGISTRY/$DOCKERHUB_NAMESPACE/ruoyi-auth:SNAPSHOT-$BUILD_NUMBER'
                sh 'docker push $REGISTRY/$DOCKERHUB_NAMESPACE/ruoyi-auth:SNAPSHOT-$BUILD_NUMBER'
              }

            }

          }
        }

        stage('推送ruoyi-gateway镜像') {
          agent none
          steps {
            container('maven') {
              withCredentials([usernamePassword(credentialsId : 'aliyun-docker-registry' ,passwordVariable : 'DOCKER_PWD_VAR' ,usernameVariable : 'DOCKER_USER_VAR' ,)]) {
                sh 'echo "$DOCKER_PWD_VAR" | docker login $REGISTRY -u "$DOCKER_USER_VAR" --password-stdin'
                sh 'docker tag ruoyi-gateway:v1.0 $REGISTRY/$DOCKERHUB_NAMESPACE/ruoyi-gateway:SNAPSHOT-$BUILD_NUMBER'
                sh 'docker push $REGISTRY/$DOCKERHUB_NAMESPACE/ruoyi-gateway:SNAPSHOT-$BUILD_NUMBER'
              }

            }

          }
        }

        stage('推送ruoyi-file镜像') {
          agent none
          steps {
            container('maven') {
              withCredentials([usernamePassword(credentialsId : 'aliyun-docker-registry' ,passwordVariable : 'DOCKER_PWD_VAR' ,usernameVariable : 'DOCKER_USER_VAR' ,)]) {
                sh 'echo "$DOCKER_PWD_VAR" | docker login $REGISTRY -u "$DOCKER_USER_VAR" --password-stdin'
                sh 'docker tag ruoyi-file:v1.0 $REGISTRY/$DOCKERHUB_NAMESPACE/ruoyi-file:SNAPSHOT-$BUILD_NUMBER'
                sh 'docker push $REGISTRY/$DOCKERHUB_NAMESPACE/ruoyi-file:SNAPSHOT-$BUILD_NUMBER'
              }

            }

          }
        }

        stage('推送ruoyi-job镜像') {
          agent none
          steps {
            container('maven') {
              withCredentials([usernamePassword(credentialsId : 'aliyun-docker-registry' ,passwordVariable : 'DOCKER_PWD_VAR' ,usernameVariable : 'DOCKER_USER_VAR' ,)]) {
                sh 'echo "$DOCKER_PWD_VAR" | docker login $REGISTRY -u "$DOCKER_USER_VAR" --password-stdin'
                sh 'docker tag ruoyi-job:v1.0 $REGISTRY/$DOCKERHUB_NAMESPACE/ruoyi-job:SNAPSHOT-$BUILD_NUMBER'
                sh 'docker push $REGISTRY/$DOCKERHUB_NAMESPACE/ruoyi-job:SNAPSHOT-$BUILD_NUMBER'
              }

            }

          }
        }

        stage('推送ruoyi-system镜像') {
          agent none
          steps {
            container('maven') {
              withCredentials([usernamePassword(credentialsId : 'aliyun-docker-registry' ,passwordVariable : 'DOCKER_PWD_VAR' ,usernameVariable : 'DOCKER_USER_VAR' ,)]) {
                sh 'echo "$DOCKER_PWD_VAR" | docker login $REGISTRY -u "$DOCKER_USER_VAR" --password-stdin'
                sh 'docker tag ruoyi-system:v1.0 $REGISTRY/$DOCKERHUB_NAMESPACE/ruoyi-system:SNAPSHOT-$BUILD_NUMBER'
                sh 'docker push $REGISTRY/$DOCKERHUB_NAMESPACE/ruoyi-system:SNAPSHOT-$BUILD_NUMBER'
              }

            }

          }
        }

        stage('推送ruoyi-monitor镜像') {
          agent none
          steps {
            container('maven') {
              withCredentials([usernamePassword(credentialsId : 'aliyun-docker-registry' ,passwordVariable : 'DOCKER_PWD_VAR' ,usernameVariable : 'DOCKER_USER_VAR' ,)]) {
                sh 'echo "$DOCKER_PWD_VAR" | docker login $REGISTRY -u "$DOCKER_USER_VAR" --password-stdin'
                sh 'docker tag ruoyi-monitor:v1.0 $REGISTRY/$DOCKERHUB_NAMESPACE/ruoyi-monitor:SNAPSHOT-$BUILD_NUMBER'
                sh 'docker push $REGISTRY/$DOCKERHUB_NAMESPACE/ruoyi-monitor:SNAPSHOT-$BUILD_NUMBER'
              }

            }

          }
        }

      }
    }

    stage('default-4') {
      parallel {
        stage('部署ruoyi-auth') {
          agent none
          steps {
            kubernetesDeploy(enableConfigSubstitution: true, deleteResource: false, kubeconfigId: "$KUBECONFIG_CREDENTIAL_ID", configs: 'ruoyi-auth/deploy/**')
          }
        }

        stage('部署ruoyi-gateway') {
          agent none
          steps {
            kubernetesDeploy(enableConfigSubstitution: true, deleteResource: false, kubeconfigId: "$KUBECONFIG_CREDENTIAL_ID", configs: 'ruoyi-gateway/deploy/**')
          }
        }

        stage('部署ruoyi-file') {
          agent none
          steps {
            kubernetesDeploy(enableConfigSubstitution: true, deleteResource: false, kubeconfigId: "$KUBECONFIG_CREDENTIAL_ID", configs: 'ruoyi-modules/ruoyi-file/deploy/**')
          }
        }

        stage('部署ruoyi-job') {
          agent none
          steps {
            kubernetesDeploy(enableConfigSubstitution: true, deleteResource: false, kubeconfigId: "$KUBECONFIG_CREDENTIAL_ID", configs: 'ruoyi-modules/ruoyi-job/deploy/**')
          }
        }

        stage('部署ruoyi-system') {
          agent none
          steps {
            kubernetesDeploy(enableConfigSubstitution: true, deleteResource: false, kubeconfigId: "$KUBECONFIG_CREDENTIAL_ID", configs: 'ruoyi-modules/ruoyi-system/deploy/**')
          }
        }

        stage('部署ruoyi-monitor') {
          agent none
          steps {
            kubernetesDeploy(enableConfigSubstitution: true, deleteResource: false, kubeconfigId: "$KUBECONFIG_CREDENTIAL_ID", configs: 'ruoyi-visual/ruoyi-monitor/deploy/**')
          }
        }

      }
    }

  }
  environment {
    DOCKER_CREDENTIAL_ID = 'dockerhub-id'
    GITHUB_CREDENTIAL_ID = 'github-id'
    KUBECONFIG_CREDENTIAL_ID = 'demo-kubeconfig'
    REGISTRY = 'registry.cn-hangzhou.aliyuncs.com'
    DOCKERHUB_NAMESPACE = 'yyyz-ruoyi'
    GITHUB_ACCOUNT = 'kubesphere'
    APP_NAME = 'devops-java-sample'
  }
  parameters {
    string(name: 'TAG_NAME', defaultValue: '', description: '')
  }
}