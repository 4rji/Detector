# Vue.js + Electron Setup Guide

This guide provides step-by-step instructions for setting up a Vue.js project with Electron, including installation, configuration, and building the application.

## Table of Contents
1. [Initialize Vue Project](#initialize-vue-project)
2. [Navigate to Project Directory](#navigate-to-project-directory)
3. [Download and Move Necessary Files](#download-and-move-necessary-files)
4. [Install Dependencies](#install-dependencies)
5. [Run Vue Development Server](#run-vue-development-server)
6. [Run Electron App](#run-electron-app)
7. [Install Electron Builder](#install-electron-builder)
8. [Build the Application](#build-the-application)
9. [Handle Build Issues in NixOS](#handle-build-issues-in-nixos)

---

## 1. Initialize Vue Project

Run the following command to initialize a Vue 3 project:

```sh
npm init vue@latest
```

Select the following options:

- Project name: `detector`
- Add TypeScript? **No**
- Add JSX Support? **No**
- Add Vue Router? **Yes**
- Add Pinia? **Yes**
- Add Vitest? **No**
- Add an End-to-End Testing Solution? **No**
- Add ESLint? **No**

---

## 2. Navigate to Project Directory

```sh
cd detector
```

---

## 3. Download and Move Necessary Files

Download the required files from GitHub:

```sh
git clone https://github.com/4rji/detector archivos
```

Move files into the correct directories:

```sh
cp archivos/App.vue src/
cp archivos/electron-main.js .
cp archivos/package.json .
mv archivos/LogViewer.vue src/components/
```

---

## 4. Install Dependencies

```sh
npm install
npm install electron --save-dev
```

---

## 5. Run Vue Development Server

Run the Vue development server in the background:

```sh
nohup npm run dev -- --port 3000 &
```

---

## 6. Run Electron App

For **NixOS**:

```sh
nix-shell -p electron nodejs_18
electron electron-main.js
```

For **other systems**:

```sh
npx electron electron-main.js
```

---

## 7. Install Electron Builder

Install Electron Builder globally:

```sh
npm install -g electron-builder
```

---

## 8. Build the Application

```sh
npm run build
```

---

## 9. Handle Build Issues in NixOS

If the build fails, run the following steps:

```sh
npm install --save-dev electron-builder
rm -rf node_modules package-lock.json
npm install
npm run dist
```

This will generate the application in the `dist/` folder.

---

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
