<script>
	import 'bootstrap/dist/css/bootstrap.min.css';
	let firstName = '';
	let surname = '';
	let email = '';
	let password = '';
	let mobile = '';
	let formSubmitted = false;
  
	function handleSubmit(event) {
	  event.preventDefault();
	  // Validate the form fields and submit data if valid
	  if (validateForm()) {
		displaySubmittedData();
		console.log('Form submitted successfully!');
		formSubmitted = true;
	  }
	}
  
	function validateForm() {
	  let isValid = true;
  
	  // Validate the form fields
	  if (firstName.length === 0 || firstName.length > 28) {
		displayError('firstName', 'First Name is required and should be less than or equal to 28 characters.');
		isValid = false;
	  } else {
		hideError('firstName');
	  }
	  
	  if (surname.length === 0 || surname.length > 28) {
		displayError('surname', 'Surname is required and should be less than or equal to 28 characters.');
		isValid = false;
	  } else {
		hideError('surname');
	  }
	  
	  if (!validateEmail(email)) {
		displayError('email', 'Invalid Email format.');
		isValid = false;
	  } else {
		hideError('email');
	  }
	  
	  if (!validatePassword(password)) {
		displayError('password', 'Invalid Password format. The password should contain at least one special character and one number.');
		isValid = false;
	  } else {
		hideError('password');
	  }
	  
	  if (!validateMobile(mobile)) {
		displayError('mobile', 'Invalid Mobile format. The mobile number should contain 10 digits.');
		isValid = false;
	  } else {
		hideError('mobile');
	  }
  
	  return isValid;
	}
  
	function validateEmail(email) {
	  // Validate the email format using a regular expression
	  const emailRegex = /^[\w-.]+@([\w-]+\.)+[\w-]{2,4}$/;
	  return emailRegex.test(email);
	}
  
	function validatePassword(password) {
	  // Validate the password format using a regular expression
	  const passwordRegex = /^(?=.*[0-9])(?=.*[!@#$%^&*])[a-zA-Z0-9!@#$%^&*]{6,15}$/;
	  return passwordRegex.test(password);
	}
  
	function validateMobile(mobile) {
	  // Validate the mobile format using a regular expression
	  const mobileRegex = /^\d{10}$/;
	  return mobileRegex.test(mobile);
	}
  
	function displayError(fieldId, errorMessage) {
	  const field = document.getElementById(fieldId);
	  const errorContainer = field.parentElement.querySelector('.error-message');
	  errorContainer.innerText = errorMessage;
	  errorContainer.style.display = 'block';
	}
  
	function hideError(fieldId) {
	  const field = document.getElementById(fieldId);
	  const errorContainer = field.parentElement.querySelector('.error-message');
	  errorContainer.style.display = 'none';
	}
  
	function displaySubmittedData() {
	  // Get the container element for displaying the submitted data
	  const submittedDataContainer = document.getElementById('submittedData');
	  
	  // Create an HTML string with the submitted data
	  const submittedDataHTML = `
		<h3>Submitted Data:</h3>
		<p><strong>First Name:</strong> ${firstName}</p>
		<p><strong>Surname:</strong> ${surname}</p>
		<p><strong>Email:</strong> ${email}</p>
		<p><strong>Password:</strong> ${password}</p>
		<p><strong>Mobile:</strong> ${mobile}</p>
	  `;
  
	  // Set the HTML of the container to display the submitted data
	 submittedDataContainer.innerHTML = submittedDataHTML;
	}
  </script>
  
  <style>
	.error-message {
	  display: none;
	  color: red;
	  font-size: 12px;
	}
  </style>
  
  <div class="container">
	<form on:submit|preventDefault={handleSubmit}>
	  <div>
		<label for="firstName" class="form-label">First Name:</label>
		<input type="text" class="form-control" id="firstName" bind:value={firstName} required>
		<div class="error-message"></div>
	  </div>
  
	  <div>
		<label for="surname" class="form-label">Surname:</label>
		<input type="text" class="form-control" id="surname" bind:value={surname} required>
		<div class="error-message"></div>
	  </div>
  
	  <div>
		<label for="email" class="form-label">Email:</label>
		<input type="email" class="form-control" id="email" bind:value={email} required>
		<div class="error-message"></div>
	  </div>
  
	  <div>
		<label for="password" class="form-label">Password:</label>
		<input type="password" class="form-control" id="password" bind:value={password} required>
		<div class="error-message"></div>
	  </div>
  
	  <div>
		<label for="mobile" class="form-label">Mobile:</label>
		<div class="input-group">
		  <span class="input-group-text">+</span>
		  <input type="tel" class="form-control" id="mobile" bind:value={mobile} required pattern="^\+?\d+$" maxlength="10">
		  <div class="error-message"></div>
		</div>
	  </div>
  
	  <h1></h1>
  
	  <button type="submit" class="btn btn-primary" disabled={!firstName || !surname || !email || !password || !mobile}>Submit</button>
	</form>
	<div id="submittedData"></div>
  </div>
	
	
  