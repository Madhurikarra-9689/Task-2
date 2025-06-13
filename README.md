# Task-1
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Internship Application | MITS</title>
  <script src="https://cdn.tailwindcss.com"></script>
</head>
<body class="bg-gray-100 text-gray-800">

  <div class="min-h-screen flex flex-col items-center justify-center p-4">
    <form id="internshipForm" class="w-full max-w-md bg-white p-6 rounded-xl shadow-md">
      <h2 class="text-2xl font-bold mb-4 text-center text-blue-700">Internship Application</h2>

      <label class="block mb-2 text-sm font-semibold">Full Name</label>
      <input type="text" name="name" required class="w-full p-2 border rounded mb-4" />

      <label class="block mb-2 text-sm font-semibold">Email</label>
      <input type="email" name="email" required class="w-full p-2 border rounded mb-4" />

      <label class="block mb-2 text-sm font-semibold">University</label>
      <input type="text" name="university" required class="w-full p-2 border rounded mb-4" />

      <button type="submit" id="submitBtn" class="w-full bg-blue-600 hover:bg-blue-700 text-white p-2 rounded">
        Submit Application
      </button>

      <p id="statusMessage" class="text-center mt-4 text-sm"></p>
    </form>

    <div class="w-full max-w-md mt-8">
      <h3 class="text-xl font-semibold mb-4">Student Applications</h3>
      <ul id="studentList" class="bg-white rounded shadow-md p-4 space-y-2"></ul>
    </div>
  </div>

  <script>
    const form = document.getElementById('internshipForm');
    const statusMessage = document.getElementById('statusMessage');
    const submitBtn = document.getElementById('submitBtn');
    const studentList = document.getElementById('studentList');

    let applicationCounter = 1;

    form.addEventListener('submit', async (e) => {
      e.preventDefault();
      statusMessage.textContent = 'Submitting...';
      statusMessage.className = 'text-center mt-4 text-sm text-gray-600';
      submitBtn.disabled = true;

      const formData = {
        name: form.name.value,
        email: form.email.value,
        university: form.university.value
      };

      try {
        await new Promise(resolve => setTimeout(resolve, 1000));

        const applicationId = applicationCounter++;
        statusMessage.textContent = `Success! Your Application ID is ${applicationId}`;
        statusMessage.className = 'text-center mt-4 text-sm text-green-600';

        const listItem = document.createElement('li');
        listItem.className = 'border p-2 rounded flex justify-between items-center';
        listItem.innerHTML = `
          <span>ID ${applicationId}: ${formData.name} - ${formData.email} - ${formData.university}</span>
          <button class="bg-red-500 text-white text-xs px-2 py-1 rounded hover:bg-red-600" onclick="this.parentElement.remove()">Delete</button>
        `;
        studentList.appendChild(listItem);

        form.reset();
      } catch (error) {
        statusMessage.textContent = 'An unexpected error occurred. Please try again later.';
        statusMessage.className = 'text-center mt-4 text-sm text-red-600';
      } finally {
        submitBtn.disabled = false;
      }
    });
  </script>

</body>
</html>
