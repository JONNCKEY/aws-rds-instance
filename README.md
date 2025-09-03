# Creación de una Instancia RDS

Descripción: Este proyecto implementa una **Instancia RDS (SQL Server)** dentro de una VPC previamente configurada en AWS.  
La solución incluye la creación de un **Security Group** y un **DB Subnet Group**, y culmina con el despliegue de la base de datos en Amazon RDS.

---

## 📌 Objetivo
Desplegar una **instancia de Microsoft SQL Server en Amazon RDS**, aprovechando una infraestructura existente en AWS (VPC con subnets, route table e internet gateway).

---

## 🏗️ Arquitectura

- VPC existente: **Lab-VPC**
- Recursos creados en este proyecto:
  - **Security Group** para RDS
  - **DB Subnet Group** para RDS
  - **Instancia RDS** (SQL Server Express Edition)

![Diagrama de arquitectura inicial](./diagrams/diagram-1.png) 

---

## 🔐 Creación del Security Group

1. Ir a **VPC → Security Groups → Crear grupo de seguridad**.
2. Configuración:
   - **Nombre**: `RDS-SecurityGroup`
   - **VPC**: `Lab-VPC`
3. Reglas de entrada:
   - Todo el tráfico desde `0.0.0.0/0`
   - MSSQL (Puerto `1433`, TCP) desde `0.0.0.0/0`

---

## 🌐 Creación del Subnet Group

1. En la consola de AWS, ir a **RDS → Subnet Groups → Create DB Subnet Group**.
2. Configuración:
   - **Name**: `RDS-SubnetGroup`
   - **VPC**: `Lab-VPC`
   - **Availability Zones**: `us-east-1a`, `us-east-1b`
   - **Subnets**: Seleccionar subnets correspondientes

---

## 💾 Creación de la Instancia RDS

1. Ir a **RDS → Databases → Create Database**.
2. Configuración:
   - **Creation method**: `Standard create`
   - **Engine type**: `Microsoft SQL Server`
   - **Edition**: `SQL Server Express Edition`
   - **Template**: `Free Tier`
   - **DB identifier**: `lab-database`
   - **Master username**: `admin`
   - **Password**: `#LabDBase3!`
   - **Instance class**: `db.t3.micro`
   - **Storage**: `General Purpose SSD (gp2)`
   - **VPC**: `Lab-VPC`
   - **DB Subnet Group**: `RDS-SubnetGroup`
   - **Public access**: `Yes`
   - **Security group**: `RDS-SecurityGroup`
   - **Availability Zone**: `us-east-1b`

---

## ✅ Validación

- La **instancia RDS** cambia a estado `Available`.
- Se obtiene el **Endpoint** para conexión.
- Se confirma la asociación con **VPC, Subnet Group y Security Group**.

![Diagrama de arquitectura final](./diagrams/diagram-2.png) 

---

## 🎯 Resultados

- Se creó exitosamente una instancia **Amazon RDS (SQL Server Express Edition)** accesible mediante el puerto `1433`.
- La infraestructura está lista para integrarse con aplicaciones o clientes SQL externos.

---

## 📂 Estructura del repositorio

Este repositorio está organizado de la siguiente manera para mantener todos los recursos del proyecto ordenados:

- `README.md`: Explica el objetivo del proyecto, los pasos realizados y resultados.
- `diagrams/`: Contiene diagramas de arquitectura o esquemas de la infraestructura.
- `screenshots/`: Almacena screenshots de la configuración en AWS para referencia visual.
