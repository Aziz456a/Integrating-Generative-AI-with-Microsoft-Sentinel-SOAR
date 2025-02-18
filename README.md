# Integrating-Generative-AI-with-Microsoft-Sentinel-SOAR


This repository showcases a graduation project that integrates the **LLaMA3 Large Language Model (LLM)** (via Hugging Face) into **Microsoft Sentinel** to enhance SOAR (Security Orchestration, Automation, and Response) capabilities. By leveraging a **Retrieval-Augmented Generation (RAG)** approach and contextual data stored in **MongoDB**, this project provides automated, context-aware responses to security incidents directly within the Sentinel interface.

---

## Table of Contents

- [Overview](#overview)  
- [Architecture](#architecture)  
- [Features](#features)  
- [Prerequisites](#prerequisites)  

---

## Overview

Modern security operations rely on **rapid** and **accurate** responses to potential threats.  
This project integrates a **LLaMA3** model (deployed via **Hugging Face**) with **Microsoft Sentinel**, enhancing the **SOAR** capabilities to provide automated, context-aware responses to security incidents.

- **Data** is stored in **MongoDB** in **vectorized** format (using **MPNet2** embeddings).  
- **Logic Apps** sends an **HTTP POST** request to an **Azure Function**, which then vectorizes the query, retrieves the most relevant context via **cosine similarity**, and augments the LLM prompt.  
- The LLM uses the **retrieved context** to generate a grounded response, which is finally displayed to the **Sentinel** user interface.

---

## Architecture

![Capture d'écran 2025-02-16 124046](https://github.com/user-attachments/assets/a4a81de3-f75b-4abb-9a4d-73b6392dec88)


1. **Request Ingestion**:  
   - **Microsoft Sentinel** detects a security incident.  
   - A **Logic App** is triggered, sending an **HTTP POST** request to the **Azure Function** endpoint.

2. **Azure Function** (RAG Pipeline):  
   - **MPNet2** is used to generate embeddings from the incoming request.   
   - **MongoDB** (vector store) is queried using **cosine similarity** to find relevant contextual data.  
   - The retrieved context is **appended** to the prompt, forming a **“super/Augmanted prompt.”**

3. **LLM Inference** (LLaMA3 via Hugging Face):  
   - The Azure Function sends the **super prompt** to the **LLaMA3** model.  
   - The model generates a **context-grounded** response.

4. **Response Delivery**:  
   - The **Azure Function** returns the LLM’s answer to **Sentinel**, which then **displays** it to the security analyst or triggers further automation steps.

---

## Features

- **Retrieval-Augmented Generation** (RAG) pipeline for context-aware LLM responses.  
- **MongoDB Vector Store** for efficient similarity search and context retrieval.  
- **Azure Function** integration with **Microsoft Sentinel** and **Logic Apps** for seamless, events based response.  
- **LLM** (LLaMA3) for generating advanced, human-like explanations and instructions in real-time.  
- **MPNet2** embeddings to ensure accurate semantic matches for context augmentation.

---

## Prerequisites
- **Azure Subscription**
- **Python 3.9 or 3.10**
- **Vs code**
- **.NET Toolkit v8 or later**
- **Azure Functions Core Tools v4** )  
- **MongoDB** (local or hosted in Azure)  
- **Hugging Face credentials and ApI** (for LLaMA3)  
- **Microsoft Sentinel** workspace (with Logic Apps configured)  
- **MPNet2** embedding model (from Hugging Face)  
