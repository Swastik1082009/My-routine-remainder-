# My-routine-remainder-
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1" />
<title>My Daily Routine Reminders</title>
<style>
  body { font-family: Arial, sans-serif; margin: 20px; background:#f4f7f8; color:#333; }
  h1 { text-align: center; color: #0275d8; }
  .routine { max-width: 600px; margin: auto; background: white; padding: 20px; border-radius: 8px; }
  .day { margin-bottom: 20px; }
  .day h2 { background: #0275d8; color: white; padding: 10px; border-radius: 5px; }
  ul { padding-left: 20px; }
  li { margin: 6px 0; }
  small { color: #666; }
</style>
</head>
<body>
<h1>My Weekly Routine & Reminders</h1>
<div class="routine">
  <div class="day">
    <h2>Weekdays (Mon, Tue, Wed, Fri)</h2>
    <ul>
      <li>6:00 AM - Wake up & morning routine</li>
      <li>6:50 AM - School bus leaves</li>
      <li>2:55 PM - Lunch + TV break</li>
      <li>3:25 PM - Homework / Board study</li>
      <li>3:47 PM - Coaching starts</li>
      <li>9:00 PM (Mon/Wed) - Guitar class</li>
      <li>10:30 PM (Mon/Wed) - Dinner + relax</li>
      <li>9:30 PM (Tue/Fri) - Board study</li>
      <li>10:30 PM (Tue/Fri) - Guitar practice (choose 2 days)</li>
      <li>12:00 AM - Sleep</li>
    </ul>
  </div>
  <div class="day">
    <h2>Thursday (No Coaching)</h2>
    <ul>
      <li>6:50 AM - School bus leaves</li>
      <li>3:30 PM - Board study session</li>
      <li>6:00 PM - Guitar practice</li>
      <li>12:00 AM - Sleep</li>
    </ul>
  </div>
  <div class="day">
    <h2>Saturday (School + Coaching)</h2>
    <ul>
      <li>6:50 AM - School bus leaves</li>
      <li>2:55 PM - Lunch + rest / TV</li>
      <li>3:30 PM - Homework / quick revision</li>
      <li>4:47 PM - Coaching starts</li>
      <li>9:00 PM (Mon/Wed) - Guitar class / practice</li>
      <li>12:00 AM - Sleep</li>
    </ul>
  </div>
  <div class="day">
    <h2>Sunday (No Coaching)</h2>
    <ul>
      <li>9:00 AM - Board study session</li>
      <li>2:00 PM - Guitar practice</li>
      <li>7:00 PM - Board study session</li>
      <li>12:00 AM - Sleep</li>
    </ul>
  </div>
</div>
<script>
  // Reminder schedule: array of reminders with time and message and days to run on
  const reminders = [
    {time: "06:00", msg: "Wake up & morning routine", days: [1,2,3,4,5]}, // Mon-Fri
    {time: "06:50", msg: "School bus leaves", days: [1,2,3,4,5,6]}, // Mon-Sat
    {time: "14:55", msg: "Lunch + TV break", days: [1,2,3,5,6]}, // Mon, Tue, Wed, Fri, Sat
    {time: "15:25", msg: "Homework / Board study", days: [1,2,3,5,6]},
    {time: "15:47", msg: "Coaching starts", days: [1,2,3,5,6]},
    {time: "21:00", msg: "Guitar class (Mon/Wed)", days: [1,3]},
    {time: "22:30", msg: "Dinner + relax (Mon/Wed)", days: [1,3]},
    {time: "21:30", msg: "Board study (Tue/Fri)", days: [2,5]},
    {time: "22:30", msg: "Guitar practice (Tue/Fri)", days: [2,5]},
    {time: "00:00", msg: "Sleep time", days: [1,2,3,4,5,6,0]},
    {time: "15:30", msg: "Board study session (Thursday)", days: [4]}, // Thursday
    {time: "18:00", msg: "Guitar practice (Thursday)", days: [4]},
    {time: "14:30", msg: "Homework / quick revision (Saturday)", days: [6]},
    {time: "16:47", msg: "Coaching starts (Saturday)", days: [6]},
    {time: "21:00", msg: "Guitar class/practice (Saturday Mon/Wed)", days: [6]},
    {time: "09:00", msg: "Board study session (Sunday)", days: [0]}, // Sunday
    {time: "14:00", msg: "Guitar practice (Sunday)", days: [0]},
    {time: "19:00", msg: "Board study session (Sunday)", days: [0]}
  ];
  // Request Notification permission on load
  if ('Notification' in window && Notification.permission !== 'granted') {
    Notification.requestPermission();
  }
  function checkReminders() {
    const now = new Date();
    const day = now.getDay(); // Sunday=0, Monday=1 ...
    const hh = now.getHours().toString().padStart(2, '0');
    const mm = now.getMinutes().toString().padStart(2, '0');
    const currentTime = hh + ":" + mm;
    reminders.forEach(reminder => {
      if(reminder.days.includes(day) && reminder.time === currentTime){
        if(Notification.permission === 'granted'){
          new Notification(reminder.msg);
        } else {
          alert(reminder.msg);
        }
      }
    });
  }
  // Check every minute
  setInterval(checkReminders, 60 * 1000);
  // Also check on load to catch missed reminders
  checkReminders();
</script>
</body>
</html>
