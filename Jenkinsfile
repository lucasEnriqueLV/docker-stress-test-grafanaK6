pipeline {
	agent { 
		docker { 
			image 'grafana/k6:latest'
			args "--entrypoint='' --net='docker-jenkins_k6'"
		}
	}
	options { ansiColor('xterm') }
	stages {
		stage("check k6") {
			steps {
				sh 'k6 version'
			}
		}
		stage("run k6 test") {
			steps {
				sh 'k6 run --vus 10 --duration 30s --out influxdb=http://influxdb:8086/k6 -e MY_HOSTNAME=${apilink} stress-test.js'
			}
		}
	}
}