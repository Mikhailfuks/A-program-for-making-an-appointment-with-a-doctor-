<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Запись к врачу</title>
    <link rel="stylesheet" href="styles.css">
</head>
<body>
    <div class="container">
        <h1>Запись к врачу</h1>
        <form id="appointmentForm">
            <input type="text" id="patientName" placeholder="Ваше имя" required>
            <input type="date" id="appointmentDate" required>
            <input type="time" id="appointmentTime" required>
            <select id="doctor">
                <option value="">Выберите врача</option>
                <option value="Семёнов С.С.">Семёнов С.С.</option>
                <option value="Петрова А.Ю.">Петрова А.Ю.</option>
                <option value="Иванова Е.Б.">Иванова Е.Б.</option>
            </select>
            <textarea id="notes" placeholder="Комментарии (по желанию)"></textarea>
            <button type="submit">Записаться</button>
        </form>
        <h2>Записи</h2>
        <div id="appointmentList"></div>
    </div>
    <script src="script.js"></script>
</body>
</html>


body {
    font-family: Arial, sans-serif;
    background-color: #f5f5f5;
    margin: 0;
    padding: 20px;
}

.container {
    max-width: 500px;
    margin: auto;
    padding: 20px;
    background: white;
    border-radius: 8px;
    box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
}

h1, h2 {
    text-align: center;
}

form {
    display: flex;
    flex-direction: column;
}

input, textarea, select {
    margin-bottom: 10px;
    padding: 10px;
    border: 1px solid #ccc;
    border-radius: 4px;
}

button {
    background-color: #28a745;
    color: white;
    border: none;
    padding: 10px;
    border-radius: 4px;
    cursor: pointer;
}

button:hover {
    background-color: #218838;
}

.appointment-item {
    background: #f8f9fa;
    margin: 10px 0;
    padding: 10px;
    border-radius: 4px;
}

.appointment-item button {
    background-color: #dc3545;
    border: none;
    padding: 5px 10px;
    border-radius: 4px;
}

.appointment-item button:hover {
    background-color: #c82333;
}


document.getElementById("appointmentForm").addEventListener("submit", function(event) {
    event.preventDefault();
    addAppointment();
});

let appointments = [];

function addAppointment() {
    const name = document.getElementById("patientName").value;
    const date = document.getElementById("appointmentDate").value;
    const time = document.getElementById("appointmentTime").value;
    const doctor = document.getElementById("doctor").value;
    const notes = document.getElementById("notes").value;

    const appointment = {
        name: name,
        date: date,
        time: time,
        doctor: doctor,
        notes: notes
    };

    appointments.push(appointment);
    displayAppointments();
    clearForm();
}

function displayAppointments() {
    const appointmentList = document.getElementById("appointmentList");
    appointmentList.innerHTML = ""; // Очистка текущих записей

    appointments.forEach((appointment, index) => {



        const appointmentItem = document.createElement("div");
        appointmentItem.className = "appointment-item";
        appointmentItem.innerHTML = `
            <h3>${appointment.name}</h3>
            <p>Врач: ${appointment.doctor}</p>
            <p>Дата: ${appointment.date}, Время: ${appointment.time}</p>
            <p>Примечания: ${appointment.notes}</p>
            <button onclick="deleteAppointment(${index})">Удалить запись</button>
        `;
        appointmentList.appendChild(appointmentItem);
    });
}

function clearForm() {
    document.getElementById("patientName").value = "";
    document.getElementById("appointmentDate").value = "";
    document.getElementById("appointmentTime").value = "";
    document.getElementById("doctor").value = "";
    document.getElementById("notes").value = "";
}

function deleteAppointment(index) {
    appointments.splice(index, 1); // Удаление записи
    displayAppointments(); // Перезагрузка списка записей
}
