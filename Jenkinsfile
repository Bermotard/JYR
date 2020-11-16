pipeline {
    agent any

    stages {
        stage('GetPokyConfAndOthers') {
            steps {
                git branch: 'zeus', url: 'git://git.yoctoproject.org/poky'
                echo "CHECKOUT git@github.com:Bermotard/Build_rasp.git -b develop build"
                checkout changelog: false, poll: false, scm: [$class: 'GitSCM', branches: [[name: '*/develop']], doGenerateSubmoduleConfigurations: false, extensions: [[$class: 'RelativeTargetDirectory', relativeTargetDir: 'build']], submoduleCfg: [], userRemoteConfigs: [[url: 'git@github.com:Bermotard/Build_rasp.git']]]
                echo "CHECKOUT -b zeus git://git.openembedded.org/meta-openembedded"
                checkout([$class: 'GitSCM', branches: [[name: '*/zeus']], doGenerateSubmoduleConfigurations: false, extensions: [[$class: 'RelativeTargetDirectory', relativeTargetDir: 'meta-openembedded']], submoduleCfg: [], userRemoteConfigs: [[url: 'git://git.openembedded.org/meta-openembedded']]])
                echo "CHECKOUT -b zeus git://github.com/96boards/meta-96boards"
                checkout([$class: 'GitSCM', branches: [[name: '*/zeus']], doGenerateSubmoduleConfigurations: false, extensions: [[$class: 'RelativeTargetDirectory', relativeTargetDir: 'meta-96boards']], submoduleCfg: [], userRemoteConfigs: [[url: 'git://github.com/96boards/meta-96boards']]])
                echo "CHECKOUT-b zeus https://github.com/IntelRealSense/meta-intel-realsense.git"
                checkout([$class: 'GitSCM', branches: [[name: '*/zeus']], doGenerateSubmoduleConfigurations: false, extensions: [[$class: 'RelativeTargetDirectory', relativeTargetDir: 'meta-intel-realsense']], submoduleCfg: [], userRemoteConfigs: [[url: 'https://github.com/IntelRealSense/meta-intel-realsense.git']]])
                echo "CHECKOUT-b zeus  git://git.yoctoproject.org/meta-raspberrypi"
                checkout([$class: 'GitSCM', branches: [[name: '*/zeus']], doGenerateSubmoduleConfigurations: false, extensions: [[$class: 'RelativeTargetDirectory', relativeTargetDir: 'meta-raspberrypi']], submoduleCfg: [], userRemoteConfigs: [[url: 'git://git.yoctoproject.org/meta-raspberrypi']]])
                echo "CHECKOUT-b zeus  git://git.yoctoproject.org/meta-selinux"
                checkout([$class: 'GitSCM', branches: [[name: '*/zeus']], doGenerateSubmoduleConfigurations: false, extensions: [[$class: 'RelativeTargetDirectory', relativeTargetDir: 'meta-selinux']], submoduleCfg: [], userRemoteConfigs: [[url: 'git://git.yoctoproject.org/meta-selinux']]])   
            }
        }
        stage('BuildRaspeberryPi'){
            steps {
                sh """export BUILDDIR=build \n
                . ./oe-init-build-env build \n
                cd $WORKSPACE/build \n
                pwd \n
                bitbake  core-image-selinux   \n 
                bitbake package-index \n"""
            }
        }
    }
}
