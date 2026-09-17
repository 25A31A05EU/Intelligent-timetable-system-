let schedules = [];

// Add a schedule
function addSchedule() {

    const section = document.getElementById("section").value;
    const subject = document.getElementById("subject").value;
    const faculty = document.getElementById("faculty").value;
    const room = document.getElementById("room").value;
    const day = document.getElementById("day").value;
    const time = document.getElementById("time").value;

    const newSchedule = {
        section,
        subject,
        faculty,
        room,
        day,
        time
    };

    const clashes = checkClashes(newSchedule);

    if (clashes.length > 0) {
        showClashes(clashes);
        return;
    }

    schedules.push(newSchedule);

    displayTimetable();

    document.getElementById("message").innerHTML =
        "<p class='success'>Schedule added successfully.</p>";

    checkAllClashes();
}


// Check for clashes
function checkClashes(newSchedule) {

    let clashes = [];

    schedules.forEach(existing => {

        if (existing.day === newSchedule.day &&
            existing.time === newSchedule.time) {

            // Faculty clash
            if (existing.faculty === newSchedule.faculty) {
                clashes.push(
                    "Faculty Clash: " +
                    newSchedule.faculty +
                    " is already assigned at this time."
                );
            }

            // Room clash
            if (existing.room === newSchedule.room) {
                clashes.push(
                    "Classroom/Lab Clash: " +
                    newSchedule.room +
                    " is already occupied."
                );
            }

            // Section clash
            if (existing.section === newSchedule.section) {
                clashes.push(
                    "Section Clash: " +
                    newSchedule.section +
                    " already has a class at this time."
                );
            }

            // Duplicate subject
            if (existing.subject === newSchedule.subject &&
                existing.section === newSchedule.section) {

                clashes.push(
                    "Subject Duplication: " +
                    newSchedule.subject +
                    " is already scheduled for this section."
                );
            }
        }
    });

    return clashes;
}


// Display timetable
function displayTimetable() {

    const body = document.getElementById("timetableBody");

    body.innerHTML = "";

    schedules.forEach(item => {

        const row = document.createElement("tr");

        row.innerHTML = `
            <td>${item.day}</td>
            <td>${item.time}</td>
            <td>${item.section}</td>
            <td>${item.subject}</td>
            <td>${item.faculty}</td>
            <td>${item.room}</td>
        `;

        body.appendChild(row);
    });
}


// Show clashes
function showClashes(clashes) {

    const box = document.getElementById("clashBox");

    box.innerHTML = "";

    clashes.forEach(clash => {

        const p = document.createElement("p");

        p.className = "warning";
        p.textContent = "⚠ " + clash;

        box.appendChild(p);
    });

    document.getElementById("message").innerHTML =
        "<p class='warning'>Schedule cannot be added because a clash was detected.</p>";
}


// Check all schedules
function checkAllClashes() {

    const box = document.getElementById("clashBox");

    let clashes = [];

    for (let i = 0; i < schedules.length; i++) {

        for (let j = i + 1; j < schedules.length; j++) {

            const a = schedules[i];
            const b = schedules[j];

            if (a.day === b.day && a.time === b.time) {

                if (a.faculty === b.faculty) {
                    clashes.push(
                        "Faculty double booking: " + a.faculty
                    );
                }

                if (a.room === b.room) {
                    clashes.push(
                        "Room/Lab double booking: " + a.room
                    );
                }

                if (a.section === b.section) {
                    clashes.push(
                        "Student/Section overlap: " + a.section
                    );
                }
            }
        }
    }

    if (clashes.length === 0) {

        box.innerHTML =
            "<p class='success'>✓ No clashes detected. Timetable is valid.</p>";

    } else {

        box.innerHTML = "";

        clashes.forEach(clash => {

            const p = document.createElement("p");

            p.className = "warning";
            p.textContent = "⚠ " + clash;

            box.appendChild(p);
        });
    }
}


// Generate sample timetable
function generateSample() {

    schedules = [

        {
            day: "Monday",
            time: "09:00 - 10:00",
            section: "CSE-A",
            subject: "Data Structures",
            faculty: "Dr. Ravi",
            room: "Room 101"
        },

        {
            day: "Monday",
            time: "10:00 - 11:00",
            section: "CSE-A",
            subject: "Java Programming",
            faculty: "Prof. Anitha",
            room: "Room 102"
        },

        {
            day: "Monday",
            time: "11:00 - 12:00",
            section: "CSE-A",
            subject: "Digital Electronics",
            faculty: "Dr. Kumar",
            room: "Room 101"
        },

        {
            day: "Tuesday",
            time: "09:00 - 10:00",
            section: "CSE-A",
            subject: "Mathematics",
            faculty: "Prof. Lakshmi",
            room: "Room 102"
        },

        {
            day: "Tuesday",
            time: "10:00 - 11:00",
            section: "CSE-A",
            subject: "Python",
            faculty: "Dr. Ravi",
            room: "Lab 1"
        }
    ];

    displayTimetable();
    checkAllClashes();

    document.getElementById("message").innerHTML =
        "<p class='success'>✓ Sample clash-free timetable generated.</p>";
}
