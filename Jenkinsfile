node {
    env.BRANCH_NAME = 'main'

    stage('Build') {
        echo 'Building...'
    }

    try {
        stage('Risky Stage') {
            error('Simulated failure!')
        }
    } catch (e) {
        echo "Caught error: ${e}"
        stage('Fallback') {
            echo 'Running fallback logic...'
        }
    } finally {
        echo 'Cleanup actions here'
    }

    stage('Test') {
        def dayOfWeek = new Date().format('u') as int
        if (dayOfWeek < 6) {
            echo 'Running tests...'
        } else {
            echo 'Skipping tests on weekend'
        }
    }

    stage('Deploy') {
        def branch = env.BRANCH_NAME ?: 'main'
        if (branch == 'main') {
            echo 'Deploying...'
        } else {
            echo "Skipping deploy, branch is ${branch}"
        }
    }
}
