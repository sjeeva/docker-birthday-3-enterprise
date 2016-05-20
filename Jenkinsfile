node ('swarm') {
    stage "Checkout Configuration Source"
    checkout scm
    
    stage "Checkout Birthday Source"
    dir("birthdaysrc") {
        git url: "https://github.com/sjeeva/docker-birthday-3.git"
    }
    
    stage "Build Birthday App"
    dir("birthdaysrc/example-voting-app") {
        sh "docker-compose -p hbswarm -f docker-compose.yml build"
    }
    
    stage "Halt Services"
    sh "docker-compose -p hbswarm down"

    stage "Configure Deployment Environment"
    sh "cp docker-compose.sd-launch.yml birthdaysrc/example-voting-app/"
    sh "cp docker-compose.sd-label.yml birthdaysrc/example-voting-app/"

    stage "Deploy Birthday App"
    dir("birthdaysrc/example-voting-app") {
        sh "docker-compose -p hbswarm -f docker-compose.sd-launch.yml up -d"
        sh "docker-compose -p hbswarm -f docker-compose.yml -f docker-compose.sd-label.yml up -d"
    }
    
    stage "Publish Birthday App details"
    dir("birthdaysrc/example-voting-app") {
        sh "docker-compose -p hbswarm ps"
    }
    
}

 
