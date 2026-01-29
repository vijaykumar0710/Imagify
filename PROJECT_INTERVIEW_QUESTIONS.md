# Imagify Project - Interview Questions for Interviewers

## **1. Architecture & Design**

### Frontend Architecture

- How did you structure your React components? Explain the folder hierarchy.
- Why did you choose to use React Context API for state management instead of Redux?
- How do you handle authentication state in your application? Walk me through the token flow.
- Describe how the Login component handles both login and signup modes.
- How do you manage user data (credits, profile info) across different pages?
- What is your routing structure? How many routes does your app have?

### Backend Architecture

- Describe your backend server structure and how you organized controllers, models, and routes.
- Why did you separate routes and controllers?
- How do you handle authentication on the backend? Explain the JWT flow.
- How does the auth middleware work? What information does it validate?
- Explain your database schema - specifically the userModel structure.
- How do you handle API errors and what's your error response format?

### Database Design

- Why did you use MongoDB? What advantages does it have for this project?
- Describe the userModel schema. What fields does it have and why?
- Do you have any database indexes? Where and why?
- How do you ensure email uniqueness in registration?
- Explain the creditBalance field - how is it initialized and updated?
- Do you have any data validation at the database level?

---

## **2. Authentication & Authorization**

- Walk me through the entire signup flow from frontend to backend.
- What happens when a user clicks "Sign Up"? Describe each step in detail.
- How do you hash passwords? Why is bcrypt better than plain hashing?
- Explain the JWT token generation process and token verification.
- What information do you store in the JWT token? Why only the userId?
- How do you persist the token on the frontend? Is localStorage secure?
- What is the auth middleware doing? Why is it needed?
- How do you handle expired tokens? What's your refresh token strategy?
- Describe the duplicate email error (E11000) - how did you handle it?
- What security measures do you have in place to prevent SQL injection or NoSQL injection?

---

## **3. Frontend Development**

### React Components

- Explain the Login component's state management. What states do you track?
- How does the "Sign Up" mode toggle work in your Login component?
- Why does the Navbar component need access to the credit context?
- How do you handle form validation in the Login component?
- What are the lifecycle hooks you use and why?
- How do you prevent the modal from scrolling the background?

### Styling

- Why did you choose Tailwind CSS over other CSS frameworks?
- How do you handle responsive design? Show examples from your navbar.
- How do you organize your Tailwind configuration?
- What's the purpose of the @tailwind directives in index.css?
- How do you handle dark mode or theme switching (if applicable)?

### Context API & State Management

- Explain your AppContext structure. What data do you store there?
- Why do you store credit as a number but initially set it to `false`?
- How does the `loadCreditsData()` function work? When is it called?
- Why do you need both `user` and `setUser` in context?
- How do you handle the token in context vs localStorage?
- What's the purpose of the `logout` function? How does it clean up?

### API Integration

- How do you make API calls to the backend? Which library do you use?
- Explain the axios configuration for API calls with authentication headers.
- How do you handle API errors and display them to users?
- What's your error handling strategy in try-catch blocks?
- How do you validate API responses before updating state?

### Performance & Optimization

- Have you implemented any performance optimizations (memoization, lazy loading)?
- How do you handle sensitive data like tokens?
- What's your strategy for preventing unnecessary re-renders?
- How do you optimize images and assets?

---

## **4. Backend Development**

### Controllers

- Explain the `registerUser` controller. What validations do you perform?
- How do you handle password hashing? Why use salt?
- In the `loginUser` controller, why do you compare passwords with bcrypt.compare()?
- What information do you return after successful login/registration?
- How do you handle the "Email already registered" error?
- Explain the `userCredits` controller. Why does it require authentication?

### Routes & Middleware

- How do you structure your routes? Why separate user and image routes?
- What's the purpose of the `userAuth` middleware?
- How does the middleware extract and verify the JWT token?
- What happens if someone calls an auth-protected route without a token?
- How do you mount routes in your main server.js file?

### Database Operations

- How do you create a new user in MongoDB?
- Explain the `findOne` method - when and why do you use it?
- How do you update user credits after image generation?
- What's the difference between `save()` and `findByIdAndUpdate()`?
- How do you handle database errors?

### Error Handling

- What happens when Mongo throws an E11000 duplicate key error?
- How do you differentiate between different types of errors?
- What's your error response format? Is it consistent?
- Do you log errors? Where and how?

---

## **5. Full-Stack Integration**

### Complete User Journey: Signup → Login → View Credits (SAMPLE ANSWER)

**Concise Answer:**

"The flow has 3 main phases:

**1. Signup & Token Generation**

- User enters credentials and submits form via axios POST to `/api/user/register`
- Backend validates input, checks for duplicate email, hashes password with bcrypt, saves to MongoDB
- Backend generates JWT token containing userId and returns it
- Frontend stores token in localStorage and context state

**2. Immediate Credit Fetch**

- After storing the token, we call `loadCreditsData()` to fetch credits
- This GET request includes token in headers for authentication
- Backend middleware verifies JWT, extracts userId, retrieves user's creditBalance from MongoDB
- Frontend receives credits and updates context

**3. Display & Persistence**

- Navbar re-renders with user's name and credit balance displayed
- Token persists in localStorage, so user stays logged in on page refresh
- On next visit, token is auto-loaded from localStorage and credits are fetched again

**Key Design Decisions:**

- JWT tokens are stateless and scale well
- localStorage persists session but can be vulnerable to XSS (httpOnly cookies preferred in production)
- Immediate credit fetch ensures UI updates don't lag
- Email validation prevents E11000 duplicate key errors from MongoDB

**What I Fixed:**

- Bug: Was using `localStorage.getItem()` instead of `setItem()` for token storage
- Race condition: Fixed timing issue between token storage and credit fetching"\*\*

---

- Explain the data flow when a user generates an image (if implemented).
- How do the frontend and backend communicate? What's the request-response cycle?
- How do you debug issues that span both frontend and backend?
- What happens when the API server is down? How does the frontend handle it?
- Explain CORS - why is it needed and how do you configure it?

---

## **6. Technical Decisions & Trade-offs**

- Why did you choose React over Vue or Angular?
- Why Vite instead of Create React App?
- Why MongoDB instead of PostgreSQL or other relational databases?
- Why Express.js for the backend?
- Why not use a library like Passport.js for authentication?
- Why Context API instead of Redux? Would you reconsider for a larger project?
- How would you scale this application if it had millions of users?

---

## **7. Bug Fixes & Problem-Solving**

### Credits Not Displaying

- What was the issue with credits not showing on screen?
- How did you debug this issue?
- Why was `localStorage.getItem()` being used incorrectly?
- How did you fix the race condition between token storage and credit fetching?
- Why did you initialize credit to `0` instead of `false`?

### Duplicate Registration Error

- Describe the E11000 error you encountered. What caused it?
- How did you prevent users from registering with duplicate emails?
- Why add a check before saving vs. relying on Mongo's unique index?
- What's the user experience when they try to register with a duplicate email?

### React/Vite Setup Issues

- What were the React DevTools warnings about?
- Why wasn't Tailwind CSS applying styles initially?
- How did you fix the JSX transformation issues?
- What's the purpose of the @vitejs/plugin-react?

---

## **8. Security & Best Practices**

- How do you store sensitive data like JWT tokens?
- Is localStorage secure? What are its vulnerabilities?
- What security headers should you add?
- How do you validate user input on the frontend and backend?
- What's your strategy for preventing CSRF attacks?
- How do you handle sensitive information in environment variables?
- Why shouldn't you store passwords in plain text?
- How do you prevent unauthorized access to protected routes?
- What's your strategy for rate limiting API endpoints?

---

## **9. Testing & Debugging**

- How do you test the signup flow? What test cases would you include?
- How would you test the authentication flow?
- What debugging tools do you use (DevTools, console, etc.)?
- How do you debug API calls that are failing?
- How would you handle integration testing between frontend and backend?
- What edge cases have you considered?

---

## **10. Deployment & DevOps**

- Where do you plan to deploy this application?
- How would you set up environment variables for production?
- What's your strategy for managing secrets (API keys, JWT secret)?
- How would you handle database backups?
- What monitoring would you implement in production?
- How do you handle zero-downtime deployments?

---

## **11. Future Improvements & Scalability**

- What features would you add next? (payment integration, image history, etc.)
- How would you handle file storage for generated images (S3, local storage)?
- How would you implement image generation (which AI service would you use)?
- What's your strategy for payment processing?
- How would you scale this to handle 10,000 concurrent users?
- Would you refactor the architecture for a larger team?
- How would you implement caching to improve performance?
- What's your strategy for API rate limiting?

---

## **12. Code Quality & Maintenance**

- How do you keep your code maintainable?
- Do you use ESLint or other linting tools?
- How do you handle code reviews?
- Do you have a style guide for your project?
- How do you document your APIs?
- What's your branching strategy?
- How do you handle dependencies and updates?
- Do you track technical debt?

---

## **13. Project-Specific Technical Details**

### Image Generation (Assumed Feature)

- How would you implement image generation?
- Which API/service would you integrate with?
- How do you handle the file storage?
- How do you charge credits per image generation?
- What's the error handling if image generation fails?

### Credit System

- How is the credit system implemented?
- When do users get initial credits?
- How do users buy more credits?
- How do you prevent credit manipulation?
- What's your billing/payment flow?

### User Flow

- Walk through the complete user experience from landing to generated image.
- How do you handle users without credits?
- What's the redirect flow after login?
- How do you handle session management?

---

## **14. Collaboration & Communication**

- How would you explain your architecture to a non-technical stakeholder?
- How do you document your code and APIs?
- How would you onboard a new developer to this project?
- What's your process for code reviews?
- How do you handle conflicting opinions on technical decisions?

---

## **15. Problem-Solving Scenarios**

- **Scenario**: A user reports that their credits disappeared. How would you investigate?
- **Scenario**: The API is timing out for 50% of requests. What's your debugging process?
- **Scenario**: You need to add a new user field. Walk me through the changes needed.
- **Scenario**: The database is growing too large. How would you optimize it?
- **Scenario**: You need to add OAuth login. How would you implement it?
- **Scenario**: A user successfully registers but then can't login. What went wrong?
- **Scenario**: The email verification is not working. How would you fix it?

---

## **Key Points to Emphasize in Your Answers**

1. **Show your debugging process** - Not just what you fixed, but how you found the issue
2. **Explain trade-offs** - Why you chose X over Y, considering pros/cons
3. **Think about scale** - How would your solution handle millions of users?
4. **Security mindset** - Always consider security implications
5. **User experience** - Show you think about the end user
6. **Code quality** - Demonstrate clean, maintainable code practices
7. **Best practices** - Show knowledge of industry standards
8. **Learning attitude** - Mention what you learned from challenges
9. **Testing** - Show you think about edge cases and testing
10. **Communication** - Explain your decisions clearly and concisely

---

## **Suggested Follow-up Questions to Ask**

- What does success look like for this role?
- How do you handle technical debt in your current projects?
- What's your code review process?
- How do you approach learning new technologies?
- What's the typical tech stack in your organization?
- How is the team structured?
- What's a recent project you worked on that you're proud of?
- How do you balance shipping features vs. code quality?
