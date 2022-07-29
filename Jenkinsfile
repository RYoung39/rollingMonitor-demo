node('slave') {
 container('jnlp-kubectl') {
 
 stage('Clone Project') {
 echo "1. Git Clone Project To Slave"
 git url: "https://github.com/RYoung39/013-cloud-homework.git"
 }
 

 stage('Prepare Environment') {
 echo "2. Prepare Environment"
 sh 'make controller-gen'
 sh 'make kustomize'
 }
 
 stage('install CRD') {
 echo "3. install CRD"
 sh 'make install'
 }
 
 stage('Build and Push Image') {
 echo "4. Build and Push Image"
 sh 'make docker-build docker-push IMG=harbor.nju.edu.cn/rollingmonitor:$BUILD_ID'
 }

  stage('Create CR') {
  echo "5. Create CR"
  sh 'kubectl apply -f config/samples/demo_v1alpha1_rollingmonitor.yaml'
  }
 
 
 }
}
