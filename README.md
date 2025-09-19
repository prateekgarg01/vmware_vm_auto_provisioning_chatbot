# 🤖 VMware VM Auto-Provisioning Chatbot

An intelligent conversational AI chatbot built with Streamlit that automates VMware vCenter virtual machine deployment through natural language interaction.

## 📋 Overview

This application combines the power of AI conversation (via Ollama) with VMware vCenter automation to create a user-friendly VM deployment experience. Users can chat naturally with the AI assistant to deploy virtual machines without needing to know complex VMware APIs or commands.

## ✨ Features

### 🤖 **AI-Powered Conversation**
- **Natural Language Processing**: Powered by Ollama AI models (default: llama3.1:8b)
- **Context-Aware Responses**: Maintains conversation history and deployment state
- **Intelligent Flow Control**: Automatically detects deployment requests and guides users through the process
- **Error Handling**: Graceful handling of AI service interruptions

### 🖥️ **VM Deployment Automation**
- **VMware vCenter Integration**: Direct API integration with vCenter REST APIs
- **Complete VM Lifecycle**: Clone, configure CPU/memory, and power on VMs
- **Step-by-Step Process**: Guided deployment flow (Name → CPU → RAM → Confirm)
- **Real-time Feedback**: Live deployment status and progress updates

### 💬 **Interactive Chat Interface**
- **Streamlit Chat Components**: Modern chat UI with message history
- **Session State Management**: Persistent conversation and deployment tracking
- **Sidebar Status Panel**: Real-time deployment progress and VM configuration display
- **Cancellation Support**: Ability to cancel deployments mid-process

## 🛠️ Technical Architecture

### **Core Components**

1. **Configuration Management**
   - Environment variable-based configuration
   - Secure credential handling
   - SSL warning suppression for internal networks

2. **VMware API Integration**
   - Session-based authentication
   - VM cloning from templates
   - Hardware configuration (CPU/Memory)
   - Power management operations

3. **AI Conversation Engine**
   - Ollama client integration
   - System prompt engineering
   - Conversation history management
   - Context-aware response generation

4. **Streamlit UI Framework**
   - Chat message components
   - Session state management
   - Sidebar information panels
   - Interactive input handling

## 📦 Dependencies

```python
streamlit     	 # Web application framework
requests      	 # HTTP client for VMware APIs
python-dotenv 	 # Environment variable management
ollama        	 # AI model client
urllib3       	 # HTTP library with SSL handling
```

## ⚙️ Configuration

### Environment Variables

Create a `.env` file in the project root:

```env
# VMware vCenter Configuration
VCENTER_URL = https://your-vcenter-server.com
VCENTER_USER = your-username
VCENTER_PASS = your-password
SOURCE_VM = vm-123456    # Source VM ID for cloning
CLUSTER = domain-123     # Target cluster ID
HOST = host-123          # Target host ID

# Ollama AI Configuration
OLLAMA_HOST = http://localhost:11434
OLLAMA_MODEL = llama3.1:8b
```

### VMware Prerequisites

1. **vCenter Access**: Valid credentials with VM provisioning permissions
2. **Source VM Template**: A configured VM template for cloning
3. **Target Infrastructure**: Identified cluster and host for VM placement
4. **Network Configuration**: Proper network access to vCenter APIs

### Ollama Setup

1. **Install Ollama**: Download and install from [https://ollama.com/)
2. **Pull Model**: Run `ollama pull llama3.1:8b`
3. **Start Service**: Ensure Ollama is running on the configured host/port

## 🚀 Installation & Usage

### Quick Start

1. **Clone/Download the code**
   
   # Save the provided code as app.py
  

2. **Install dependencies**
   ```bash
   pip install -r requirements.txt
   ```

3. **Configure environment**
   
   Create .env file with your VMware and Ollama settings
   

4. **Run the application**
   
   streamlit run app.py
  

5. **Access the interface**
   - Open your browser to `http://localhost:8501`
   - Start chatting with the AI assistant

### Usage Flow

1. **Normal Conversation**
   - Chat naturally with the AI assistant
   - Ask questions, get help, or have general conversations

2. **VM Deployment Process**
   - Say "deploy a VM" or similar phrases to start
   - Follow the guided 4-step process:
     - **Step 1**: Provide VM name
     - **Step 2**: Specify CPU cores
     - **Step 3**: Set RAM amount (GB)
     - **Step 4**: Confirm deployment

3. **Monitor Progress**
   - Watch the sidebar for real-time status updates
   - View current VM configuration
   - Cancel deployment if needed

## 🔧 Code Structure

### **Main Functions**

#### VMware API Functions
```python
get_vmware_token()           # Authenticate with vCenter
clone_vm(vm_name, token)     # Clone VM from template
patch_cpu(vm_id, cpu, token) # Configure CPU cores
patch_memory(vm_id, ram, token) # Configure memory
power_on(vm_id, token)       # Start the VM
deploy_vm_agent()            # Orchestrate full deployment
```

#### AI Conversation

chat_with_agent()            # Handle AI conversation and context


#### Streamlit UI Components
- Session state initialization
- Chat message display
- User input handling
- Deployment flow logic
- Sidebar status panel

### **State Management**

The application uses Streamlit's session state to maintain:
- `chat_history`: Conversation messages
- `deployment_step`: Current deployment phase
- `vm_details`: VM configuration (name, CPU, RAM)

### **Deployment States**
- `normal`: Regular conversation mode
- `ask_name`: Requesting VM name
- `ask_cpu`: Requesting CPU cores
- `ask_ram`: Requesting RAM amount
- `confirm`: Awaiting deployment confirmation

## 🎯 Key Features Explained

### **Intelligent Conversation Flow**
The AI assistant can seamlessly switch between normal conversation and deployment mode based on user intent. It uses keyword detection to identify deployment requests and maintains context throughout the process.

### **Robust Error Handling**
- VMware API errors are caught and reported user-friendly messages
- AI service interruptions are handled gracefully
- Input validation ensures proper VM specifications

### **Real-time Status Updates**
The sidebar provides live updates on:
- Current deployment step
- VM configuration details
- Deployment progress
- Quick access to cancellation

### **Natural Language Processing**
The system uses advanced AI to:
- Understand user intent
- Generate contextual responses
- Provide deployment confirmations
- Handle conversational nuances

## 🔒 Security Considerations

### **Credential Management**
- All sensitive credentials stored in environment variables
- SSL verification disabled for internal networks (configurable)

### **API Security**
- Session-based authentication with vCenter
- Input validation for all user-provided data

## 🚨 Troubleshooting

### **Common Issues**

1. **AI Connection Errors**
   - Verify Ollama is running: `ollama list`
   - Check OLLAMA_HOST configuration
   - Ensure model is downloaded: `ollama pull llama3.1:8b`

2. **VMware API Errors**
   - Verify vCenter credentials and permissions
   - Check network connectivity to vCenter
   - Validate SOURCE_VM, CLUSTER, and HOST IDs

3. **Streamlit Issues**
   - Clear browser cache
   - Restart the Streamlit application
   - Check for port conflicts

