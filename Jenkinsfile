node ('swarm') {
    stage "Checkout Configuration Source"
    checkout scm
    
    stage "Checkout Birthday Source"
    dir("birthdaysrc") {
        git url: "https://github.com/sjeeva/docker-birthday-3.git"
    }
    
    stage "Build Birthday App"
    dir("birthdaysrc/example-voting-app") {
        sh "docker-compose -f docker-compose.yml build"
    }
    
    stage "Halt Services"
    dir("birthdaysrc/example-voting-app") {
        sh "docker-compose -f docker-compose.yml -f docker-compose.sd-label.yml down"
        sh "docker-compose -p serv -f docker-compose.sd-launch.yml down"
    }

    stage "Configure Deployment Environment"
    sh "cp docker-compose.sd-launch.yml birthdaysrc/example-voting-app/"
    sh "cp docker-compose.sd-label.yml birthdaysrc/example-voting-app/"

    stage "Deploy Birthday App"
    dir("birthdaysrc/example-voting-app") {
        sh "docker-compose -p serv -f docker-compose.sd-launch.yml up -d"
        sh "docker-compose -f docker-compose.yml -f docker-compose.sd-label.yml up -d"
    }
    
    stage "Scale Birthday App"
    dir("birthdaysrc/example-voting-app") {
        sh "docker-compose -f docker-compose.yml -f docker-compose.sd-label.yml scale voting-app=3"
        sh "docker-compose -f docker-compose.yml -f docker-compose.sd-label.yml scale result-app=2"
    }
    
    stage "Publish Birthday App details"
    dir("birthdaysrc/example-voting-app") {
        sh "docker-compose -p serv -f docker-compose.sd-launch.yml ps"
        sh "docker-compose ps"
    }
}
