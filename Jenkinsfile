node('php'){
    stage('Clean'){
        deleteDir()
        sh 'ls -la'
    }
    
    stage('Fetch') {
        checkout scm
    }
    
    stage('Build'){
        sh 'composer install --prefer-dist --no-dev --ignore-platform-reqs'
        //sh 'php artisan config:cache'
        // sh 'php artisan route:cache'
    }
    
    stage('config'){
        parallel(
            'config cache':{
                sh 'php artisan config:cache'
            },
            'config route':{
                sh 'php artisan route:cache'
            }
        )
    }
    
    stage('Docker Build') {
        sh 'docker build -t alan1978/todoapi:$BUILD_NUMBER .'
    }
    
    stage('Docker Ship') {
        sh 'docker push alan1978/todoapi:$BUILD_NUMBER'
    }
}
