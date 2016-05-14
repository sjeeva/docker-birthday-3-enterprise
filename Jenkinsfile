node ('docker') {
    stage "Checkout Birthday Source"
    dir("birthdaysrc") {
        git url: "https://github.com/sjeeva/docker-birthday-3.git"
    }
    
    stage "Build Birthday"
    sh "ls -l"
    dir("birthdaysrc/example-voting-app") {
        sh "ls -l"
        # sh "docker-compose -p autong -f docker-compose.yml build"
    }
    
}

 
