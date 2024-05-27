<h1>Title - Creating a CI/CD Pipeline to "Deploy a React App on GitHub Pages" using GitHub Actions</h1>

<h3>Prerequisites</h3> - (1) React App Code - It should be working on localhost
                (2) Basic Knowledge of React and node.js 
                (3) Basic Knowledge of how CI/CD works and what is the need for this.

<h3>Task</h3> - We are going to create a Automatic Workflow to deploy the code from a GitHub Page.

<h3>Steps</h3> -

      Step 01 : Create a folder and start a react app e.g 'myapp' in it.
      Step 02 : Clone any react app code from GIT. For this instance i've used "https://github.com/devopsproin/github-actions-crash-course.git"
      Step 03 : Run the code in vs code and start the server using 'npm start' in terminal.
      Step 04 : Now the server must be running on localhost:3000
      Step 05 : Now create a ".github/workflows/deploy.yaml" file and paste this workflow in this.

                        name: CI/CD for React App                      // Name of the WorkFlow

                        on:                                            // Triggering the Workflow 
                            push:                                      // Workflow will be triggered on push event on main or master branch
                                 branches: [main, master]
                            workflow_dispatch:                         // Workflow can be triggered manaually as well

                        permissions:                                   // Permission to write the content in gh-pages branch
                            contents: write

                        jobs:                                          // Job will decide what work will be done in this workflow
                            build_and_deploy:
                                runs-on: ubuntu-latest                 // Ubuntu-latest server will be selected to do this job

                                steps:

                                    - name: Checkout Repository        // To checkout to the Present Repository where the code is available
                                      uses: actions/checkout@v3

                                    - name: Setup node.js              // To set-up the node environment on the server for this repo
                                      uses: actions/setup-node@v3
                                      with:
                                          node-version: 18             // node-version specified

                                    - name: Install Dependencies       // Installing the Dependencies
                                      run: npm install

                                    - name: Build Project              // Building the project in build folder
                                      run: npm run build

                                    - name: Deploy to GitHub Pages     // Deploying the code to GitHub Pages in gh-pages branch                   
                                      uses: JamesIves/github-pages-deploy-action@4.1.0
                                      with:
                                          branch: gh-pages
                                          folder: build

      Step 06 : Push the code to GitHub and Check the Actions tab - 'CI/CD for React App' action must be triggered

      Step 07 : Now to set the deployement using GitHub Pages.

                Go to Setting --> Pages --> Deploy from a branch --> select gh-pages and then save.

                There must be one more action run automatically.

                It'll provide the Link to access the App.

     Step 08 : To set the Homepage of the app, go to code --> Package.json --> add  "homepage": "https://sanjayaaswani.github.io/react-test-app/",

                provide the link given at pages tab in place of "https://sanjayaaswani.github.io/react-test-app/"

     Step 09 : Now check the link, code must be running.

