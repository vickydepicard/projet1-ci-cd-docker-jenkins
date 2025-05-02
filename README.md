# docker-jenkins-projet1

## ✨ Description du projet

Projet d'intégration continue et de déploiement continu (CI/CD) utilisant Docker et Jenkins.
Ce projet a pour but de mettre en place une chaîne d'automatisation complète pour le build, le test et le déploiement d'une application conteneurisée dans différents environnements (dev, test, prod).

---

## 📁 Structure du projet

```
projet1/
├── docker/
│   ├── dev/
│   │   └── Dockerfile
│   ├── test/
│   │   └── Dockerfile
│   └── prod/
│       └── Dockerfile
├── src/                    # Code source de l'application
├── .github/workflows/      # Pour GitHub Actions (si utilisé en plus de Jenkins)
├── Jenkinsfile             # Pipeline Jenkins
├── README.md
```

---

## ⚙️ Technologies utilisées

* [Docker](https://www.docker.com/) : Conteneurisation de l'application
* [Jenkins](https://www.jenkins.io/) : Intégration et déploiement continus (CI/CD)
* [GitHub](https://github.com/) : Gestion de code source
* Bash : Pour automatiser certaines tâches

---

## ⚡ Prérequis

* Docker et Docker Compose installés
* Jenkins installé en local (ou sur un serveur)
* Git

---

## ▶️ Exécution du projet

### 1. Cloner le projet

```bash
git clone https://github.com/ton-utilisateur/docker-jenkins-projet1.git
cd docker-jenkins-projet1
```

### 2. Lancer Jenkins (si nécessaire)

```bash
docker run -d -p 8081:8080 -p 50000:50000 \
  -v jenkins_home:/var/jenkins_home \
  -v /var/run/docker.sock:/var/run/docker.sock \
  --name jenkins jenkins/jenkins:lts
```

### 3. Accéder à Jenkins

Naviguer sur : [http://localhost:8081](http://localhost:8081)

### 4. Configurer le pipeline Jenkins

* Créer un nouveau *Pipeline project*
* Sélectionner le mode **Pipeline script from SCM**
* Renseigner le repo GitHub et le chemin vers le `Jenkinsfile`

---

## 📝 Contenu du Jenkinsfile (extrait)

```groovy
pipeline {
    agent any

    stages {
        stage('Cloner le repo') {
            steps {
                git 'https://github.com/ton-utilisateur/projet1.git'
            }
        }

        stage('Construire l\'image Docker') {
            steps {
                script {
                    docker.build('monapp:dev', './docker/dev')
                }
            }
        }

        stage('Lancer le conteneur') {
            steps {
                sh '''
                    docker stop monapp-dev || true
                    docker rm monapp-dev || true
                    docker run -d --name monapp-dev -p 8080:80 monapp:dev
                '''
            }
        }
    }
}
```

---

## 📆 Feuille de route

* [x] Conteneurisation de l'application
* [x] Mise en place d'un pipeline Jenkins simple
* [ ] Ajout de tests automatisés
* [ ] Déploiement vers environnement de test
* [ ] Intégration avec GitHub Actions (optionnel)

---

## 🚀 Objectifs pédagogiques

* Comprendre le fonctionnement d'une chaîne CI/CD avec Jenkins et Docker
* Savoir structurer un projet Docker multi-environnements (dev, test, prod)
* Maîtriser la définition et l'exécution d'un `Jenkinsfile`

---

## ✌️ Auteur

Hotio Hen Vicky De Picard

---

## ⚖️ Licence

Ce projet est sous licence MIT - voir le fichier [LICENSE](LICENSE) pour plus d’informations.

