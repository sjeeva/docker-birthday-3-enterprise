node ('docker') {
    stage "Checkout Configuration Source"
    checkout scm
    
    stage "Checkout Birthday Source"
    dir("birthdaysrc") {
        git url: "https://github.com/sjeeva/docker-birthday-3.git"
    }
    
    stage "Build Birthday App"
    dir("birthdaysrc/example-voting-app") {
        sh "docker-compose -p autong -f docker-compose.yml build"
    }
    
    stage "Deploy Birthday App"
    sh "cp docker-compose.basic.yml birthdaysrc/example-voting-app/"
    dir("birthdaysrc/example-voting-app") {
        sh "docker-compose -p autong -f docker-compose.yml -f docker-compose.basic.yml stop"
        sh "docker-compose -p autong -f docker-compose.yml -f docker-compose.basic.yml rm -f"
        sh "docker-compose -p autong -f docker-compose.yml -f docker-compose.basic.yml up -d"
    }
    
    stage "Publish Birthday App details"
    dir("birthdaysrc/example-voting-app") {
        sh "docker-compose -p autong -f docker-compose.yml -f docker-compose.basic.yml ps"
    }
    
}

 
