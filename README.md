import React, { useState } from 'react';

const MyForm = () => {
  const [name, setName] = useState('');
  const [email, setEmail] = useState('');
  const [phone, setPhone] = useState('');

  const handleSubmit = async (event) => {
    event.preventDefault();
    try {
      const response = await fetch(`https://example.com/api/user?email=${email}`);
      const data = await response.json();
      if (data.exists) {
        alert('User Found');
      } else {
        const createUserResponse = await fetch('https://example.com/api/user', {
          method: 'POST',
          headers: {
            'Content-Type': 'application/json'
          },
          body: JSON.stringify({
            name,
            email,
            phone
          })
        });
        const createdUserData = await createUserResponse.json();
        alert('User Created Successfully');
      }
    } catch (error) {
      console.error(error);
    }
  };

  return (
    <form onSubmit={handleSubmit}>
      <label htmlFor="name">Name:</label>
      <input type="text" id="name" required value={name} onChange={(event) => setName(event.target.value)} />
      <label htmlFor="email">Email:</label>
      <input type="email" id="email" required value={email} onChange={(event) => setEmail(event.target.value)} />
      <label htmlFor="phone">Phone:</label>
      <input type="tel" id="phone" required value={phone} onChange={(event) => setPhone(event.target.value)} />
      <button type="submit">Submit</button>
    </form>
  );
};

export default MyForm;
