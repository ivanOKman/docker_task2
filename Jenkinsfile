
try {
node('host') {
    stage('\u27A1 Preparation (Checking out)') {
		env.Stage = 'Preparation (Checking out)'
		git changelog: false, poll: false, url: 'https://github.com/spring-guides/gs-spring-boot.git'
	}
	stage('\u27A1 Building code') {
		env.Stage = 'Building code'
		sh '''alias gradle='docker run --rm -v $(pwd):$(pwd) -w $(pwd) gradle gradle'
		cd initial
		gradle build'''
	}
}       // node end
} catch (hudson.AbortException exc) {
        env.Msg = """
		Build ABORTED on stage "$Stage"
		Trace: $exc
		"""
        echo "$Msg"

} catch (err) {
		currentBuild.result = 'FAILURE'
		env.Msg = """
		Build FAILED on stage "$Stage"
		Trace: $err
		"""
		echo "$Msg"
}
