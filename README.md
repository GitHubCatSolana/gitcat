# gitcat
First ever github cat
ca: https://pump.fun/profile/B6i6Q83gNtv4L3GuJBJNaqoMgco2SBNvqPE68yDx318i

chat
// Connect to the WebSocket server
const socket = new WebSocket('ws://githubcat8080.com');

// Get references to DOM elements
const messages = document.getElementById('messages');
const messageInput = document.getElementById('messageInput');
const sendButton = document.getElementById('sendButton');

// Function to add a message to the chat window
function addMessage(message, sender) {
    const messageElement = document.createElement('div');
    messageElement.textContent = `${sender}: ${message}`;
    messages.appendChild(messageElement);
    messages.scrollTop = messages.scrollHeight;
}

// Send message when send button is clicked
sendButton.addEventListener('click', () => {
    const message = messageInput.value;
    if (message) {
        addMessage(message, 'You');
        socket.send(message);
        messageInput.value = '';
    }
});

// Send message when Enter key is pressed
messageInput.addEventListener('keypress', (event) => {
    if (event.key === 'Enter') {
        sendButton.click();
    }
});

// Receive messages from the WebSocket server
socket.addEventListener('message', (event) => {
    addMessage(event.data, 'Server');
});

// Handle WebSocket connection open
socket.addEventListener('open', () => {
    console.log('Connected to the WebSocket server');
});

// Handle WebSocket connection close
socket.addEventListener('close', () => {
    console.log('Disconnected from the WebSocket server');
});

// Handle WebSocket errors
socket.addEventListener('error', (error) => {
    console.error('WebSocket error:', error);
});
