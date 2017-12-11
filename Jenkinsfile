node("docker") {
    docker.withRegistry('https://quay.io/repository/hansriezebos/spoed_hap', '<<your-docker-registry-credentials-id>>') {
    
        git url: "https://github.com/hansriezebos/levelup.git", credentialsId: 'fd2241d2-19b7-4263-a222-3d0f0de53d2a	'
    
        sh "git rev-parse HEAD > .git/commit-id"
        def commit_id = readFile('.git/commit-id').trim()
        println commit_id
    
        stage "build"
        def app = docker.build "my-project-name"
    
        stage "publish"
        app.push 'master'
        app.push "${commit_id}"
    }
}