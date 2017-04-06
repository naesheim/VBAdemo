@Library('SharedLibrary@master') _

node {
    stage('CheckoutNewRepo'){
	       def repo='project'
	       checkoutRepo repo
    }
    
    stage('EchoOut') {
		def output = 'Mundoss!'
		hello output
    }
}
