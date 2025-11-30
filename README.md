# Darkroom Gallery App 

Hey! Welcome to my **Darkroom Gallery** project. This is a simple Node.js application where you can upload and view images. It's built with Express, MongoDB, and EJS for the frontend. It's Main goal is to test Pipelines.


##  Features

- **Image Upload**: Upload your favorite photos.
- **Gallery View**: See all uploaded images in a nice grid.
- **DevOps Magic**: Fully automated CI/CD pipeline using Jenkins.

##  How to Run Locally

If you want to play around with the code on your machine:

1.  **Clone the repo**:
    ```bash
    git clone https://github.com/iammuirurimaina/gallery.git
    cd gallery
    ```

2.  **Install dependencies**:
    ```bash
    npm install
    ```

3.  **Start the server**:
    ```bash
    node server.js
    ```
    Then open your browser at `http://localhost:3000`.

##  The DevOps Pipeline (Jenkins)

I've set up a **Jenkins pipeline** that does all the heavy lifting automatically whenever I push code:

1.  **Checkout**: Grabs the latest code from GitHub.
2.  **Verify**: Checks that Node.js and npm are installed.
3.  **Install**: Installs all the project dependencies.
4.  **Test**: Runs the automated tests (`npm test`). If they fail, I get an **email notification**! 📧
5.  **Deploy**: If everything looks good, it checks my live site on **Render**.
6.  **Notify**: Once deployed successfully, it sends a message to my **Slack channel** with the Build ID and the live link! 💬

## 🌐 Live Demo

Check out the live application here:
-> [https://gallery-ian.onrender.com/](https://gallery-ian.onrender.com/)

##  Milestones Completed

- **Milestone 1**: Project Setup
- **Milestone 2**: Basic Pipeline (Build & Deploy)
- **Milestone 3**: Automated Tests & Email Alerts
- **Milestone 4**: Slack Integration 

---
*Built by Ian Maina*
