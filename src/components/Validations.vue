<script>
 export const isValidPassword = (password) => {
  // Password length should be at least 8 characters
  if (password.length < 8) {
    return false;
  }

  // Regular expressions for checking password criteria
  const uppercaseRegex = /[A-Z]/;
  const lowercaseRegex = /[a-z]/;
  const digitRegex = /[0-9]/;
  const specialCharRegex = /[!@#$%^&*()_+\-=\[\]{};':"\\|,.<>\/?]/;

  // Check if password meets all criteria
  return (
    uppercaseRegex.test(password) &&
    lowercaseRegex.test(password) &&
    digitRegex.test(password) &&
    specialCharRegex.test(password)
  );
};
export const isValidEmail = (email) => {
  // Regular expression for email validation
  const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
  return emailRegex.test(email);
};
</script>