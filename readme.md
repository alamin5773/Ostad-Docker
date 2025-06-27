# Ostad Project

This repository contains two separate projects:

- **Ostadserver** — An Express.js backend server
- **OstadUI** — A React frontend application built with Vite

---

## Prerequisites

Make sure you have the following installed on your system:

- [Node.js](https://nodejs.org/) (version 16 or above recommended)
- npm (comes with Node.js) or yarn

---

## Getting Started

### 1. Run Ostadserver (Express Backend)

```bash
cd Ostadserver
npm install
npm start
```

This will start the Express server, usually on `http://localhost:5000` (or your configured port).

---

### 2. Run OstadUI (React + Vite Frontend)

```bash
cd OstadUI
npm install
npm run dev
```

This will start the Vite development server, usually on `http://localhost:3000` (or your configured port).

---

## Notes

- Make sure your backend server (`Ostadserver`) is running before starting the frontend (`OstadUI`) if your frontend depends on any API from the backend.
- You can customize ports by editing the `package.json` scripts or configuration files (`vite.config.js` for frontend and `server.js` or equivalent for backend).
- For production builds:

  - Backend: Use `npm run build` if applicable or deploy as needed.
  - Frontend: Run `npm run build` inside `OstadUI` to create a production build.

---

## Useful Commands

| Command         | Description                      | Location    |
| --------------- | -------------------------------- | ----------- |
| `npm install`   | Install dependencies             | Both        |
| `npm start`     | Start Express server             | Ostadserver |
| `npm run dev`   | Start Vite development server    | OstadUI     |
| `npm run build` | Build production frontend bundle | OstadUI     |

---


# Kubernetes YAML Descriptions

This README provides a short description of each Kubernetes YAML configuration file used in the deployment.

## Files and Descriptions

- **namespace.yaml**: Defines a custom namespace (`alamin-ns`) to isolate the resources within the cluster.

- **mongo-configmap.yaml**: Contains configuration data (e.g., database name) for MongoDB that can be injected into the pods as environment variables.

- **mongo-secret.yaml**: Stores sensitive data such as MongoDB username and password securely, which are used by the MongoDB and Mongo Express deployments.

- **mongo-deployment.yaml**: Defines the Deployment for the MongoDB instance, specifying container image, environment variables, and resource configuration.

- **mongo-service.yaml**: Exposes the MongoDB deployment as a ClusterIP service so that it can be accessed internally within the Kubernetes cluster.

- **mongo-express-deployment.yaml**: Defines the Deployment for Mongo Express, a web-based MongoDB admin interface.

- **mongo-express-service.yaml**: Exposes Mongo Express as a ClusterIP service to be accessible from within the cluster or via ingress.

- **backend-deployment.yaml**: Describes the deployment of the backend application, including image configuration and environment settings.

- **backend-service.yaml**: Exposes the backend application internally using a ClusterIP service.

- **frontend-deployment.yaml**: Defines the deployment for the frontend application (student registration UI), including build image and port details.

- **frontend-service.yaml**: Exposes the frontend UI application inside the cluster or through an ingress.

- **ingress.yaml**:  
  Defines Ingress rules to expose multiple services under a single domain (`ostad.local`). It uses path-based routing to forward traffic to the correct service:
  - `/` → `ostad-ui` service (port 5173)  
  - `/api` → `ostad-server` service (port 5050)  
  - `/mongo` → `mongo-express` service (port 8081)  
  Requires an Ingress controller (e.g., NGINX) to be set up in the cluster.
