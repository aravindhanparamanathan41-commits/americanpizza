# Security Features

This document outlines the security measures implemented in the American Pizza application.

## Backend Security

### 1. **Helmet.js** - Security Headers
- Sets various HTTP headers to help protect the app from well-known web vulnerabilities
- Content Security Policy (CSP) configured
- XSS protection enabled
- Frame options set to prevent clickjacking

### 2. **Rate Limiting**
- **Authentication endpoints**: 5 requests per 15 minutes per IP
- **Order creation**: 10 requests per minute per IP
- **General API**: 100 requests per 15 minutes per IP
- Prevents brute force attacks and DoS attempts

### 3. **Input Validation & Sanitization**
- **express-validator**: Validates all user inputs
- **express-mongo-sanitize**: Prevents MongoDB injection attacks
- Email validation with normalization
- Password strength requirements (min 8 chars, uppercase, lowercase, number)
- XSS protection through string sanitization
- Request size limits (10MB max)

### 4. **CORS Configuration**
- Restricted to specific origin (not wildcard in production)
- Credentials support enabled
- Limited HTTP methods allowed
- Specific headers whitelist

### 5. **JWT Security**
- Token expiration (7 days)
- Issuer and audience validation
- Secure token verification
- Proper error handling without information leakage

### 6. **Password Security**
- bcryptjs for password hashing (10 rounds)
- Minimum 8 characters required
- Must contain uppercase, lowercase, and number
- Passwords never returned in API responses

### 7. **Error Handling**
- Generic error messages to prevent information leakage
- Detailed errors logged server-side only
- No stack traces exposed to clients

### 8. **MongoDB Security**
- Input sanitization prevents NoSQL injection
- Query result limits to prevent DoS
- Proper ID validation (MongoDB ObjectId format)

## Frontend Security

### 1. **Token Storage**
- JWT tokens stored in localStorage (consider httpOnly cookies for production)
- Tokens never logged or exposed in URLs

### 2. **Input Validation**
- Client-side validation for better UX
- Server-side validation is the source of truth
- XSS protection through React's built-in escaping

### 3. **API Communication**
- HTTPS enforced in production
- Secure headers from backend
- CORS protection

## Security Best Practices

### Environment Variables
- Never commit `.env` files
- Use strong, random secrets in production
- Rotate secrets periodically

### Production Checklist
- [ ] Set `NODE_ENV=production`
- [ ] Use strong `JWT_SECRET` (32+ characters)
- [ ] Configure proper `CLIENT_ORIGIN`
- [ ] Enable HTTPS
- [ ] Set up proper logging and monitoring
- [ ] Configure firewall rules
- [ ] Regular security updates
- [ ] Database backups
- [ ] Rate limiting tuned for production load

### Password Requirements
- Minimum 8 characters
- At least one uppercase letter
- At least one lowercase letter
- At least one number
- Maximum 128 characters

### API Security
- All admin endpoints require authentication
- Input validation on all user inputs
- Rate limiting on sensitive endpoints
- Request size limits
- Proper error handling

## Reporting Security Issues

If you discover a security vulnerability, please report it responsibly:
1. Do not create a public issue
2. Contact the development team privately
3. Provide detailed information about the vulnerability
4. Allow time for the issue to be addressed before public disclosure

## Security Updates

This application should be regularly updated to address:
- Dependency vulnerabilities (use `npm audit`)
- Security patches
- New security best practices
- Framework updates




