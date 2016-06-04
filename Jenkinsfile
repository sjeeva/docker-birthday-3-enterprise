node ('swarm') {
    stage "Checkout Deployment Architecture and Operations Source"
    checkout scm
    
    stage "Checkout Developer Source Code"
    dir("${env.DEVPROJROOTDIR}") {
        git url: "${env.DEVPROJROOTURL}"
    }
    
    stage "Configure Deployment Environment"
    sh "cp docker-compose.sd-launch.yml ${env.DEVPROJCOMPOSEDIR}"
    sh "cp docker-compose.sd-label.yml ${env.DEVPROJCOMPOSEDIR}"
    
    stage "Build Application"
    dir("${env.DEVPROJCOMPOSEDIR}") {
        sh "docker-compose -f docker-compose.yml build"
    }
    
    stage "Halt Deployed Services"
    dir("${env.DEVPROJCOMPOSEDIR}") {
        sh "docker-compose -f docker-compose.yml -f docker-compose.sd-label.yml down"
        sh "docker-compose -p serv -f docker-compose.sd-launch.yml down"
    }

    stage "Deploy Birthday App"
    dir("${env.DEVPROJCOMPOSEDIR}") {
        sh "docker-compose -p serv -f docker-compose.sd-launch.yml up -d"
        sh "docker-compose -f docker-compose.yml -f docker-compose.sd-label.yml up -d"
    }
    
    stage "Scale Birthday App"
    dir("${env.DEVPROJCOMPOSEDIR}") {
        sh "docker-compose -f docker-compose.yml -f docker-compose.sd-label.yml scale voting-app=3"
        sh "docker-compose -f docker-compose.yml -f docker-compose.sd-label.yml scale result-app=2"
    }
    
    stage "Publish Birthday App details"
    dir("${env.DEVPROJCOMPOSEDIR}") {
        sh "docker-compose -p serv -f docker-compose.sd-launch.yml ps"
        sh "docker-compose ps"
    }
}
