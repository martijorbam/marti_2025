---
layout: page 
title: Study Planner
permalink: /cptproject
description: CPT
---

<div>
  <!-- INPUT FORM -->
  <div>
    <h2>Add Session</h2>
    <div>
      <input id="sub" type="text" placeholder="Subject" />
      <input id="dur" type="number" placeholder="Duration (minutes)" />
      <input id="note" type="text" placeholder="Notes" />
      <button onclick="addSession()">Add Session</button>
    </div>
  </div>

  <!-- DISPLAY SAVED SESSIONS -->
  <div>
    <h2>Saved Sessions</h2>
    <ul id="sessionList"></ul>
  </div>
  <!-- CLEAR SAVED SESSIONS -->
  <button onclick="clearSessions()">Clear All Sessions</button>

</div>

<script>
// List where all sessions will be stored
  const sessionList = document.getElementById('sessionList');

  function loadSessions() {
    const sessions = JSON.parse(localStorage.getItem('sessions')) || [];
    sessionList.innerHTML = "";

    if (sessions.length === 0) {
      sessionList.innerHTML = "<li>No sessions saved yet!</li>";
    } else {
      sessions.forEach((s, index) => {
        const item = document.createElement('li');
        item.innerHTML = `
          <strong>${index + 1}. Subject:</strong> ${s.subject}<br>
          <strong>Duration:</strong> ${s.duration} minutes<br>
          <strong>Notes:</strong> ${s.notes}
        `;
        sessionList.appendChild(item);
      });
    }
  }


// Function to clear previous sessions
    function clearSessions() {
    localStorage.removeItem('sessions'); // Removes only the sessions data
    loadSessions(); // Re-loads the session list (it will be empty now)
    alert("All sessions have been cleared!");
    }

// Function to add a new session
  function addSession() {
    const subject = document.getElementById('sub').value.trim();
    const duration = document.getElementById('dur').value.trim();
    const notes = document.getElementById('note').value.trim();

// Check if inputs are valid
    if (!subject || !duration || isNaN(duration)) {
      alert("Please enter valid subject and duration.");
      return;
    }

// Create a new session and add it to the list
    const session = { subject, duration: parseInt(duration), notes };
    const sessions = JSON.parse(localStorage.getItem('sessions')) || [];
    sessions.push(session);

// Save updated sessions list back to localStorage
    localStorage.setItem('sessions', JSON.stringify(sessions));

// Send message based on planned study time
    let totalMinutes = 0;
    sessions.forEach(s => {
      totalMinutes += s.duration;
    });

    if (totalMinutes > 180) {
      alert("Great job! You've planned over 3 hours of study. Remember to take breaks!");
    } else if (totalMinutes > 60) {
      alert("Nice! You've scheduled over an hour. Keep it up!");
    }

// Clear the input fields
    document.getElementById('sub').value = "";
    document.getElementById('dur').value = "";
    document.getElementById('note').value = "";

// Reload sessions to update displayed list
    loadSessions();
  }

// Call loadSessions when the page loads
  window.onload = loadSessions;
</script>
