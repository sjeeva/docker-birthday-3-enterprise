node ('docker') {
    stage "Checkout Configuration Source"
    checkout scm
    
    stage "Checkout Birthday Source"
    dir("birthdaysrc") {
        git url: "https://github.com/sjeeva/docker-birthday-3.git"
    }
    
    stage "Build Birthday"
    sh "ls -l"
    dir("birthdaysrc/example-voting-app") {
        sh "ls -l"
        sh "echo docker-compose -p autong -f docker-compose.yml build"
    }
    
}

 
