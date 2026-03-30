
## **Fedora RamaLama Task: Model Execution & Troubleshooting**

Project Objective
The goal of this task is to demonstrate the ability to run Large Language Models (LLMs) on Fedora using the RamaLama tool. 
I explored two models registries (Hugging Face and Ollama) and documented the process of managing local OCI-compliant model storage.

## **Technical Environment**
OS: Fedora Linux

Environment: VirtualBox VM

Tool: RamaLama CLI (v0.17.1)

Hardware: 8GB RAM / Btrfs Filesystem

## **Successful Model Runs**
**Ollama Registry (TinyLlama)**
I successfully pulled and ran the TinyLlama model using the ollama:// transport. 
The model correctly identified the four foundations of the Fedora Project (Software, Community, Integration, and Delivery).

Command: ramalama run ollama://tinyllama "What are the four foundations of the fedora project?" despite a tiny typo the model was able to inteprate what the question was and give an answer.

![Ollama Success Screenshot](images/success_ollama_tinyllama)

## **Hugging Face Registry (IBM Granite)**
I also executed the IBM Granite 3.0 model using the hf:// transport to verify cross-registry compatibility.

Command: ramalama run hf://ibm-granite/granite-3.0-2b-instruct "What are the four foundations of the fedora project?" used same typo to see if model was able to inteprate

![Hugging Face Granite Success](images/success_huggingface_granite)

## **Local Storage & Troubleshooting**
One of the most important parts of this task was managing local model assets and resolving versioning errors.

Audit of Local Models
Using the list command, I verified which models were cached locally to avoid redundant downloads and metadata timeout errors.

Command: ramalama list

![RamaLama List Audit](images/local_model_audit)

## **Resolving Version Mismatches**
During the task, I encountered "does not exist" errors when attempting to run specific versions (e.g., Granite 3.1 vs 3.0). By auditing the local store and matching the transport string exactly to the cached model, I successfully resolved the execution path.

![Troubleshooting Version Mismatch](images/troubleshooting_version_mismatch)

## **Key Takeaways**
RamaLama effectively handles different registries (hf:// and ollama://) seamlessly.

Offline Execution: Using the --pull=never flag is a powerful way to run models in a fresh VM environment once the OCI blobs are cached.

Error Handling: Paying close attention to model naming conventions in the Hugging Face registry is critical for successful CLI execution.

