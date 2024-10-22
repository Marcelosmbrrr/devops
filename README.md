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

<img src="https://grafana.com/api/dashboards/3834/images/2403/image" width="500" />

### Prometheus - Data Collecting

Prometheus is a monitoring tool that excels at collecting system and application metrics in real-time.

Prometheus uses a pull-based metric collection model, where it makes HTTP requests to endpoints exposed by applications. The route "/metrics" is being used on this project.

The <a href="https://prometheus.io/docs/instrumenting/clientlibs/" target="_blank">client libraries</a> are libraries that help implement data collection in applications. 

This project is using the third party library <a href="https://spatie.be/docs/laravel-prometheus/v1/introduction">Spatie Laravel-Prometheus</a> that configures the PHP client library in laravel.

For services that do not expose metrics natively (such as databases, servers, etc.), exporters are used, they are custom collectors.

### Grafana - Data Visualization

Grafana is a data analysis and visualization platform that allows you to create <a href="https://grafana.com/grafana/dashboards/" target="_blank">interactive and customizable dashboards</a>. It integrates with multiple data sources, including Prometheus, to provide rich visualizations and insights into the metrics collected.

### Usage

They were integrated into the project via Docker. To test them, simply run the docker-compose.yml file. 
Prometheus is accessible on localhost:9090, while Grafana can be accessed on localhost:3000.

```
docker-compose -f docker-compose.yml up -d
````

To access the Prometheus dashboard, go to localhost:9090 and click on "Status -> Targets" to view the status of the configured endpoints in prometheus.yml.

Next, access the Grafana dashboard at localhost:3000 using the credentials "admin" for both username and password. Go to "Connections" and "Data Sources" to add a new data source, selecting Prometheus and entering the URL http://prometheus:9090.

Once configured, Grafana will receive data from Prometheus! You can also use a custom dashboard by going to "Dashboards," clicking "New -> Import," and entering the ID of a dashboard available on the Grafana website, like <a href="https://grafana.com/grafana/dashboards/3662-prometheus-2-0-overview/">this one</a>.

## Jenkins

soon ..

## Github Actions

GitHub Actions é uma ferramenta de automação integrada ao GitHub que permite criar fluxos de trabalho (workflows) para automatizar tarefas relacionadas ao desenvolvimento de software.

- Workflows: Arquivos YAML no diretório .github/workflows, acionados por eventos como push ou pull request.
- Jobs e Steps: Workflows contêm jobs (executados em paralelo ou sequência) compostos por steps (tarefas individuais).
- Ações: Blocos de construção que podem ser ações da comunidade ou criadas por você.
- Ambientes e Variáveis: Permitem definir variáveis e usar segredos para informações sensíveis.
- Integração: Funciona com diversas ferramentas, facilitando automações em todo o processo de desenvolvimento.
