node {

    stage('Descargar codigo') {
        def mvnHome = tool 'M3'
        env.PATH = "${mvnHome}\\bin;${env.PATH}"
        checkout scm
        bat "mvn clean compile"
    }

    stage('Instalar') {
        bat "mvn install -Dmaven.test.skip=true"
    }


stage('Copiar archivos') {

            
        script {
            // Ruta del servidor de destino en WildFly
            def wildflyDeployDir = 'C:\\Servers\\wildfly-30.0.1.Final\\standalone\\deployments'

            // Copiar archivos al directorio de implementación de WildFly
            bat "xcopy /Y /I /E target\\*.war \"${wildflyDeployDir}\""


        }
   
}

stage('reiniciar servidor') {
            // Detener y reiniciar Wildfly
    try {
        bat "net stop Wildfly"
    } catch (Exception e) {
        echo "El servicio Wildfly no estaba en ejecución, continuando..."
    }
 
    bat "net start Wildfly"
}
}