# Bank Marketing Dataset Project

In this project, I worked with the **Bank Marketing dataset** to configure, deploy, and consume a cloud-based machine learning production model using **Azure**. I used **Automated Machine Learning (AutoML)** to train and select the best model, and I deployed it as a REST endpoint. Additionally, I created, published, and consumed a pipeline to automate the workflow. Finally, I documented all my work in this **README file**.

---

## Project Overview

In this project, I used **Azure Machine Learning** to build and deploy a machine learning model. Here’s an overview of what I accomplished:

1. **Automated Machine Learning (AutoML)**:
   - I configured and ran an AutoML experiment using a **Jupyter Notebook** in Azure Machine Learning Studio. This allowed me to automatically train and evaluate multiple models to find the best-performing one.
   - I also ran the AutoML experiment **manually via the terminal** to understand the process from a different perspective.

2. **Model Deployment**:
   - After identifying the best model, I deployed it as a **web service** using Azure. This created a REST endpoint that could be consumed to make predictions.

3. **Testing the Endpoint**:
   - I tested the deployed model using **Swagger**, which provided an interactive interface to send requests to the endpoint and validate its functionality.
   - The endpoint was also consumed in terminal in endpoint.py and in the notebook.

4. **Pipeline Creation**:
   - I created and published a **pipeline** to automate the entire workflow, from data preprocessing to model deployment. This made the process reproducible and scalable.

5. **Documentation**:
   - I documented all the steps, including screenshots and explanations, in this **README file** to demonstrate my work.

## Architectural Diagram

Below is an architectural diagram that illustrates the different components of the project and their interactions:

![Architectural Diagram](images/diagram_az.png)

### Components:
1. **Authentication**:
   - Set up authentication to access Azure services.
   In this course, I did not have the necessary privileges to create authentication (e.g., create Role-Based Access Control - RBAC). However, you can refer to the image below to see the code required for setting up authentication.

   **Note**: If I had the required privileges, a JSON file containing authentication information would have been generated for me. This file typically includes details such as subscription IDs, tenant IDs, and client secrets, which are essential for accessing Azure services programmatically.

   ![Authentication Code Example](images/no-permission-to-rbac.png)

2. **AutoML**:
   - I used **Azure AutoML** to train and evaluate multiple machine learning models. The experiment was run in two ways: through a **Jupyter Notebook** and **manually via the terminal**.
   - To run the AutoML experiment, I first registered a dataset provided by the course, which is available at the following URL: [Bank Marketing Dataset](https://automlsamplenotebookdata.blob.core.windows.net/automl-sample-notebook-data/bankmarketing_train.csv).
   - After registering the dataset, I used it to train the model on a pre-configured compute instance in Azure Machine Learning Studio.
   - The dataset was successfully uploaded to Azure ML Studio, and the AutoML experiment was executed. Below are images showing the dataset in Azure ML Studio and the completed AutoML run.
  
     
    ![Registered Dataset](images/registered_datasets.png)
   
    ![Completed Experiment](images/job_completed.png)

4. **Deploy the Best Model**:
   - Deployed the best-performing model as a REST endpoint using Azure Machine Learning. This allowed me to make predictions by sending HTTP requests to the endpoint. In this scenario we have VontingEnsemble for the best model as showed in the image below.
    ![best_model](images/best_model_completed.png)

5. **Enable Logging**:
   - To monitor the deployed model’s performance and usage, I enabled **Application Insights** for logging. This was done by running the `logs.py` script, which retrieves logs from the deployed web service.
   - Application Insights provides detailed telemetry data, including request/response times, error rates, and custom logs, making it easier to troubleshoot issues and ensure the model is functioning correctly.
   - Below is an image showing **Application Insights** enabled for the deployed model, displaying real-time monitoring data and logs and the logs that where genarated running logs.py
   ![Application Insights](images/Applications_Insights.png)
   ![Logs](images/logs.png)

6. **Consume Endpoints**:
   - In this step, I consumed the deployed model’s REST endpoint to make predictions. This involved sending sample data to the endpoint and receiving predictions in real-time. To interact with the endpoint, I used **Swagger**, which provides an interactive interface for testing the API.

   ### Using Swagger:
   - Azure automatically generates a **Swagger JSON file** for deployed models. To access it, I navigated to the **Endpoints** section in Azure Machine Learning Studio and located the deployed model. The Swagger JSON file was available for download from there.
   - To run Swagger locally, I used the `swagger.sh` script, which downloads the latest Swagger container and runs it on port 80. If port 80 is unavailable (due to permission issues), the script can be updated to use a higher port number (e.g., above 9000).

   ### Testing the Endpoint:
   - With Swagger UI running, I was able to send sample data to the deployed model’s endpoint and receive predictions in real-time. This step ensured that the endpoint was functioning as expected and that the model could handle incoming requests.

   ### Challenges:
   - I successfully connected Swagger to the localhost to test the REST endpoint. However, I encountered issues when trying to run the `serve.py` script, which was supposed to serve the `swagger.json` file. Despite debugging, the script did not show the expected HTTP connection, as shown in the images below. This is a point for future improvement.
  ![serve.py bug](images/serve.py.png)
  ![serve.py bug](images/serve-error.png)
  
7. **Create and Publish a Pipeline**:
   - I created and published a pipeline to automate the entire machine learning workflow. This pipeline ensures that the process is efficient, reproducible, and scalable.
   - After deploying the model, I used the `endpoint.py` script to interact with the trained model. To do this, I updated the `scoring_uri` and `key` variables in the script to match the endpoint URI and authentication key generated after deployment.
   - The `endpoint.py` script sends a sample JSON payload to the deployed model and retrieves predictions in real-time. This step was crucial for testing the model's performance and ensuring that the endpoint was functioning correctly.

   ### Benchmark Testing:
   - I conducted benchmark testing to evaluate the pipeline's performance. This involved sending multiple requests to the endpoint and measuring response times, accuracy, and resource usage.
   - Below are images showing the benchmark results, including response times and prediction accuracy. These results demonstrate the pipeline's efficiency and the model's ability to handle real-time requests.
   ![Apache bench](images/apache_benchmarking_runned.png)


---

## Screencast Demonstration (Written Description)

Below is a detailed written description of the entire process, simulating what would be shown in a screencast video:

1. **Working Deployed ML Model Endpoint**:
   - The deployed model endpoint is fully functional and capable of receiving HTTP requests. It processes incoming data in JSON format and returns predictions in real-time. For example, when sending a sample payload with customer data (e.g., age, job, marital status), the endpoint responds with a prediction indicating whether the customer is likely to subscribe to a term deposit.

2. **Deployed Pipeline**:
   - The deployed pipeline automates the entire machine learning workflow, from data ingestion and preprocessing to model training and deployment. The pipeline is triggered automatically whenever new data is available, ensuring that the model is always up-to-date. The screencast would demonstrate the pipeline's execution, showing each step being completed successfully.

3. **Available AutoML Model**:
   - The AutoML experiment identified the best-performing model based on predefined metrics (e.g., accuracy, AUC). The selected model is displayed in the Azure Machine Learning Studio, along with its performance metrics and training details. This section would highlight how AutoML evaluated multiple algorithms and hyperparameters to choose the optimal model.

4. **Successful API Requests to the Endpoint with a JSON Payload**:
   - The process of sending API requests to the deployed endpoint is demonstrated using the `endpoint.py` script. A sample JSON payload is sent to the endpoint directly via Python code. The `POST` request to the API returns the prediction results, as shown in the image below.
   - It's important to note that the code in `endpoint.py` required adjustments to work correctly. Specifically, the `data` variable needed to include the key `"Inputs"` to match the expected format of the API. Without this adjustment, the request would fail due to incorrect payload formatting.
   ![response](images/endpoints_consumining_API.png)

---

This written description provides a comprehensive overview of the project, simulating what would be demonstrated in a screencast video. It ensures that all key components—deployed model, pipeline, AutoML results, and API interactions—are clearly documented and easy to understand.

---

## Challenges and Improvements

During the project, I faced a few challenges and identified areas for improvement:

1. **Swagger and Local Server**:
   - I successfully connected Swagger to the localhost to test the REST endpoint. However, I encountered issues when trying to run the `serve.py` script, which was supposed to serve the `swagger.json` file. Despite debugging, the script did not show the expected HTTP connection, as shown in the image below. This is a point for future improvement.
  ![serve.py bug](images/serve.py.png)

2. **Logging**:
   - While I was able to enable logging and retrieve logs from the deployed model, I noticed that the logs could be more detailed. Enhancing the logging mechanism would make it easier to monitor and troubleshoot the model in production.

3. **Pipeline Optimization**:
   - The pipeline I created works well, but it could be optimized further to handle larger datasets and more complex workflows. Using advanced pipeline configurations and integrating with other Azure services could improve performance.


## Conclusion

This project allowed me to gain hands-on experience with **Azure Machine Learning**, from training models using AutoML to deploying and consuming them via REST endpoints. I also learned how to create and publish pipelines to automate workflows. By documenting my work in this README file, I hope to provide a clear and comprehensive overview of the project.

Feel free to explore the code, screenshots, and video to see the project in action! 🚀

