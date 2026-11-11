
pipeline{
   agent any

   environment {
        SONAR_PROJECT_KEY = 'LLMopsRuchi'
        SONAR_SCANNER_HOME = tool 'SonarQube Scanner'
//         AWS_REGION = 'us-east-1'
//         ECR_REPO = 'my-repo'
//         IMAGE_TAG = 'latest'
 }

  stages{
       stage('Cloning Github repo to Jenkins'){
          steps{
            script{
                echo 'Cloning Github repo to Jenkins.......'
                checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[credentialsId: 'LLMOps1', url: 'https://github.com/rkajalglobal/Multi-LLMOps.git']])

                 }
            }
       }
  

      stage('SonarQube Analysis') {
            steps {
                withCredentials([string(credentialsId: 'SonarQube-Token', variable: 'SONAR_TOKEN')]) {
                    withSonarQubeEnv('SonarQube Env') {
                        sh '''
                            ${SONAR_SCANNER_HOME}/bin/sonar-scanner \
                            -Dsonar.projectKey=${SONAR_PROJECT_KEY} \
                            -Dsonar.sources=. \
                            -Dsonar.host.url=http://sonarqube-dind:9000 \
                            -Dsonar.token=${SONAR_TOKEN}
                        '''
                    }
                }
            }
        }

//     stage('Build and Push Docker Image to ECR') {
//                                              steps {
//                                                 withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', credentialsId:]])
//                                                     script {
//                                                        def accountId = sh(script: "aws sts get-caller-identity -- query Account"
//                                                        def ecrUrl = "${accountId}.dkr.ecr.${env.AWS_REGION}.amazonaws.com/${en}"

//                                                           sh """
//                                                          aws ecr get-login-password -- region ${AWS_REGION} | docker login -- user
//                                                          docker build -t ${env.ECR_REPO} :${IMAGE_TAG} .
//                                                          docker tag ${env.ECR_REPO}:${IMAGE_TAG} ${ecrUrl}:${IMAGE_TAG}
//                                                          docker push ${ecrUr1}:${IMAGE_TAG}
//                                                              """
//                                                            }
//                                                       }
//                                                   }
//                                            }

//        stage('Deploy to ECS Fargate') {
//                                        steps {
//                                            withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', credentialsId: 'aws-to']])
//                                              script {
//                                                   sh """
//                                                 aws ecs update-service \
//                                                 -- cluster multi-ai-agent-cluster \
//                                                 -- service multi-ai-agent-def-service-shqlo39p
//                                                 -- force-new-deployment \
//                                                 -- region ${AWS_REGION}
//                                                      """
//                                                      }
//                                                 }
//                                              }
//                                         }

            }                                
                          
  }
