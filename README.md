# Peer-to-Peer Network Communication and File Sharing

## 1. Overview

This project is a desktop-based Peer-to-Peer (P2P) messaging and file-sharing application developed using Python, TCP sockets, and Tkinter. It enables users to exchange text messages and files directly between peers without relying on a central server.

Each running application acts as an independent peer that can accept incoming connections and establish outgoing connections with other peers over a network. The application uses multithreading to manage network communication efficiently while maintaining a responsive graphical user interface.

## 2. Features

* **Peer Initialization:** Start a peer with a custom name and a specified listening port.
* **Peer Connection:** Connect to another peer using its IP address and port number.
* **Peer Management:** View connected peers and select a destination for communication.
* **Text Messaging:** Send and receive text messages directly between connected peers.
* **File Sharing:** Transfer files between peers over TCP connections.
* **File Management:** Save received files in the `downloads/` directory while preventing existing files from being overwritten.
* **Multithreading:** Perform network operations in background threads to prevent the graphical interface from freezing.
* **Message Framing:** Use length-prefixed JSON messages for structured communication between peers.

## 3. Project Structure

```text
p2p_network/
├── main.py             # Tkinter graphical user interface
├── p2p_node.py         # Peer connections, messaging, and file transfers
├── protocol.py         # Length-prefixed JSON message framing
├── README.md           # Project documentation
├── requirements.txt    # External dependency list
├── downloads/          # Directory for received files
├── .gitignore          # Excludes unnecessary files from version control
└── .venv/              # Optional Python virtual environment
```

The `.gitignore` file excludes the virtual environment, Python cache files, and received files stored in the `downloads/` directory. The virtual environment is optional and does not need to be included in version control.

## 4. System Requirements

The following requirements must be met to run the application:

* Python 3.11 or later.
* Tkinter for the graphical user interface.
* An operating system that supports Python TCP socket programming.
* No third-party Python packages are currently required.

### Verify Python Installation

Open Command Prompt or PowerShell and execute:

```powershell
python --version
```

This command displays the installed Python version.

### Verify Tkinter Availability

Run the following command:

```powershell
python -m tkinter
```

If Tkinter is installed correctly, a small test window will appear. Close the window before continuing.

## 5. Installation and Setup

### Step 1: Open the Project Directory

Open Command Prompt or PowerShell and navigate to the directory containing the project files.

### Step 2: Create a Virtual Environment

A virtual environment is recommended to keep the project environment separate from other Python projects.

Create the environment using:

```powershell
python -m venv .venv
```

### Step 3: Activate the Virtual Environment

On Windows, execute:

```powershell
.venv\Scripts\activate
```

If you are using Linux or macOS, execute:

```bash
source .venv/bin/activate
```

Alternatively, you can run the application using your existing Python installation without activating a virtual environment.

### Step 4: Install Dependencies

The project currently does not require any third-party packages, so installing additional dependencies is unnecessary. Tkinter must be available in your Python installation.

## 6. Running the Application

From the project directory, execute:

```powershell
python main.py
```

The application window will open with default values for the peer name and listening port.

Follow these steps to start the application:

1. Enter a unique peer name.
2. Specify an available listening port.
3. Click **Start Peer** to begin accepting incoming connections.
4. Connect to another peer by entering its IP address and listening port.
5. Select a connected peer from the peer list before sending messages or files.
6. Click **Stop Peer** when you want to stop listening and disconnect from connected peers.

Keep the application running while communicating with other peers.

## 7. Connecting Two Peers on the Same Computer

The application can be tested by running two separate instances on the same computer.

### Step 1: Start the First Peer

Launch the application using `python main.py`. Set the listening port to `5000` and click **Start Peer**.

### Step 2: Start the Second Peer

Open another terminal in the same project directory and launch a second application instance:

```powershell
python main.py
```

Set its listening port to `5001` and click **Start Peer**.

### Step 3: Establish the Connection

In the second application instance, enter the following connection details:

* **IP Address:** `127.0.0.1`
* **Remote Port:** `5000`

Click **Connect** to establish a connection with the first peer.

### Step 4: Exchange Messages and Files

After the connection is established, select the connected peer from the peer list. You can now send text messages and transfer files between the two application instances.

The first peer listens on port `5000`, while the second peer listens on port `5001`. Each instance maintains its own listening port and can communicate with connected peers.

## 8. Connecting Peers Over a Local Network

To communicate between two different computers, connect both devices to a network that allows direct peer-to-peer communication.

Follow these steps:

1. Start the application on the receiving computer and click **Start Peer**.
2. Identify the receiving computer's reachable IP address.
3. Ensure that the listening port is accessible through the network and permitted by the firewall.
4. Start the application on the sending computer.
5. Enter the receiving computer's IP address and listening port.
6. Click **Connect** to establish the connection.

The application requires the target peer's IP address and port to establish a connection. It does not currently support automatic peer discovery or Internet NAT traversal.

## 9. Messaging and File Transfer

### Text Messaging

To send a message, select a peer from the **Connected Peers** list, enter the message, and use the messaging controls to send it.

Messages and relevant network events appear in the **Messages / Events** log.

### File Sharing

To transfer a file:

1. Select the intended recipient from the connected peer list.
2. Click **Choose File & Send**.
3. Select the file you want to transfer.
4. Allow the transfer to complete.

The receiving peer saves the file in the `downloads/` directory. If a file with the same name already exists, the application generates a numbered filename to avoid overwriting the existing file.

### Communication Protocol

The application uses TCP sockets for reliable, ordered data delivery between connected peers.

Control messages are encoded as JSON and transmitted using length-prefixed framing. File contents are transferred as raw bytes over the established TCP connection, with file data sent in chunks.

The `protocol.py` module manages message framing, while `p2p_node.py` handles peer connections, messaging, and file transfers.

## 10. Troubleshooting

* **The application does not start:** Verify that Python 3.11 or later is installed and available from the terminal.
* **The graphical interface does not open:** Check whether Tkinter is installed and properly configured. On Linux, you may need to install the appropriate Tkinter package separately.
* **The peer cannot start:** Ensure the listening port is between `1` and `65535` and is not already being used by another application.
* **The connection fails:** Verify that the remote peer is running, has started listening, and is using the correct IP address and port.
* **The connection is blocked:** Check the firewall settings and confirm that the network permits inbound TCP connections on the selected port.
* **The file is not received:** Verify that the connection remains active, that the transfer completes successfully, and that the application has permission to write to the `downloads/` directory.
* **Python cannot find the project files:** Make sure the terminal is opened in the project directory before executing `python main.py`.

## 11. Security and Limitations

This project is intended for educational purposes and demonstrates the fundamental concepts of peer-to-peer networking, socket programming, multithreading, and file sharing.

The current implementation has the following limitations:

* **No Encryption:** Communication is not protected by end-to-end encryption.
* **No Authentication:** The application does not verify the identity of connecting peers.
* **No Automatic Peer Discovery:** Users must manually provide the target peer's IP address and port.
* **No Internet NAT Traversal:** Direct connections across networks may fail when routers or firewalls prevent inbound connections.
* **Limited Security Protection:** The application is not designed for handling sensitive information over untrusted networks.

Users should avoid transferring confidential files or sensitive information until appropriate security measures, including encryption, authentication, and input validation, have been implemented.

## 12. Conclusion

The Peer-to-Peer Network Communication and File Sharing application demonstrates how Python TCP sockets can be used to build a decentralized communication system. By combining direct peer connections, text messaging, file transfers, JSON-based message framing, multithreading, and a Tkinter graphical interface, the project provides a practical introduction to network application development.

The project also offers a foundation for future improvements, such as secure communication, peer authentication, automatic peer discovery, and enhanced file-transfer management.


