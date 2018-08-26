podTemplate(containers: [
    containerTemplate(
        name: 'dind',
        image: 'docker:stable-dind',
        privileged: true,
        resourceLimitMemory: '2Gi',
        resourceRequestCpu: '1',
        resourceRequestMemory: '1Gi'),
    containerTemplate(
        name: 'docker',
        image: 'docker:latest',
        privileged: false,
        resourceLimitMemory: '2Gi',
        resourceRequestCpu: '1',
        resourceRequestMemory: '1Gi',
        ttyEnabled: true,
        command: 'cat')
    ],
    label: 'test',
    volumes: [
        emptyDirVolume(memory: false, mountPath: '/var/run'),
    ]
)
{
    node('test') {
        container('docker') {
            sh 'pwd'
            sh 'apk add git'
            sh 'git clone https://github.com/tao-zhang/ansible-role-jenkins.git'
            sh 'docker run -v `pwd`:`pwd` -w `pwd` alpine ls -lh'
            
            docker.image("python:3.7-alpine").inside() {
                sh 'pwd'
                sh 'python -V'
            }
        }
    }
}

