# Terraform Como subir uma instancia na AWS

## Instalando o Terraform no seu terminal

Para fazer a instalação do Terraform no meu caso estou utilizando o S.O Windows, utlilizei o gerenciador de pacote Chocolatey:

`` bash 
Set-ExecutionPolicy Bypass -Scope Process -Force; [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://community.chocolatey.org/install.ps1'))
``
Para instalar o terraform

`` bash
choco install terraform
terraform -help
``

## Instalando o Docker

Para ter acesso a CLI da AWS, instalei o docker para instalar o nginx. Fiz a instalação do docker segunda a documentação para windows.

Utlilizei os seguintes comando:



terraform {
  required_providers {
    docker = {
      source  = "kreuzwerker/docker"
      version = "~> 3.0.1"
    }
  }
}

provider "docker" {
  host    = "npipe:////.//pipe//docker_engine"
}

resource "docker_image" "nginx" {
  name         = "nginx"
  keep_locally = false
}

resource "docker_container" "nginx" {
  image = docker_image.nginx.image_id
  name  = "tutorial"

  ports {
    internal = 80
    external = 8000
  }
}

``


