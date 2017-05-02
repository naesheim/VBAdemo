@Library('SharedLibrary@master') _

node {
    stage('CheckoutNewRepo'){
	       def repo='DjangoRichie'
	       checkoutRepo repo
    }

    stage('EchoOut') {
		def output = 'Mundoss!'
		hello output
    }
}
