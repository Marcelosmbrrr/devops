# About

This project is built with Laravel 11 to explore the integration of advanced DevOps tools throughout the development and production lifecycle. The objective is explore the essential of modern DevOps practices.

## Gitflow

<img src="https://velog.velcdn.com/images/boseong-choi/post/59173dfa-fb90-49b4-8323-daa5a38ca02b/image.png" width="500" />

GitFlow is a branching model for Git that helps teams manage their code more easily. It sets up a clear way to handle different stages of development, like building new features, prepping for releases, and fixing bugs.

There are commands for every step, like "git flow init" for initializing, "git flow feature start name" and "git flow feature start finish" for feature development, "git flow release start x.y.z" and "git flow release finish x.y.z -m 'message'" for releases etc.

- Master/Main: This is where your production-ready code lives.
- Develop: This is where all the new features come together before they go live.
- Feature: Use this branch for working on new features. It is created from develop and merge into it.
- Release: This is for getting everything ready for production. Is created from develop and merge into it and main.
- Hotfix: Quick fixes can be made here when something needs urgent attention. Is created from main, merge into it and develop.

By utilizing GitFlow, learn the fundamental development workflow associated with this approach and technology, which is seamlessly integrated and ready to use within Git.

## SonarQube

<img src="https://www.opcito.com/sites/default/files/inline-images/5%20(1).png" width="500" />

SonarQube is an open-source platform used for continuous inspection of code quality. It helps developers manage code quality by identifying bugs, vulnerabilities, and code smells in their projects.

SonarQube can be seamlessly integrated with Jenkins, a popular continuous integration and continuous delivery (CI/CD) tool. This integration allows you to automatically analyze your code after each build.

Initially, to test it, run the command below. 

```
docker-compose -f docker-compose.sonar.yml up -d
````

Then, acessing the sonarqube dashboard on port 9000 with the credentials 'admin' and 'admin', is possible to create a new project and a token. After this step, fill the fields with the respective values and run the command:

```
docker run \
	--rm \
	--network=host \
	-e SONAR_HOST_URL="http://127.0.0.1:9000" \
	-e SONAR_SCANNER_OPTS="-Dsonar.projectKey=project_name" \
	-e SONAR_TOKEN="secret_token" \
	-v "project_absolute_local_path:/usr/src" \
	sonarsource/sonar-scanner-cli
````

## Prometheus and Grafana

### Prometheus - data collecting

Prometheus is a monitoring tool that excels at collecting system and application metrics in real-time.

Prometheus uses a pull-based metric collection model, where it makes HTTP requests to endpoints exposed by applications. For example, "/metrics" is a commonly used endpoint.

The <a href="https://prometheus.io/docs/instrumenting/clientlibs/" target="_blank">client libraries</a> are libraries that help implement data collection in applications. There are for Java, PHP, Ruby, Nodejs, and several others. 

For services that do not expose metrics natively (such as databases, servers, etc.), exporters are used, ...

### Grafana - data visualization

Grafana is a data analysis and visualization platform that allows you to create interactive and customizable dashboards. It integrates with multiple data sources, including Prometheus, to provide rich visualizations and insights into the metrics collected.

## Amazon AWS

soon...

## Pipeline with Jenkins

soon...
