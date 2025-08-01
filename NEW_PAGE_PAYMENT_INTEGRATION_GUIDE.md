# 🚀 Payment Integration Guide for New HTML Pages

## 📋 **Quick Setup Checklist**

For every NEW HTML page that needs payment functionality, follow this checklist:

### ✅ **Step 1: Copy Required Scripts**
Add these scripts to your `<head>` or before closing `</body>`:

```html
<!-- Stripe.js Library -->
<script src="https://js.stripe.com/v3/"></script>

<!-- Firebase SDK (if using authentication) -->
<script src="https://www.gstatic.com/firebasejs/9.0.0/firebase-app-compat.js"></script>
<script src="https://www.gstatic.com/firebasejs/9.0.0/firebase-auth-compat.js"></script>
<script src="https://www.gstatic.com/firebasejs/9.0.0/firebase-firestore-compat.js"></script>
```

### ✅ **Step 2: Copy Configuration Constants**
Add these exact configurations (DO NOT CHANGE):

```javascript
const STRIPE_CONFIG = {
    publishableKey: 'pk_live_51Rr5H03QiDHRr52effkP2HrTynAiO7NYD8VQfmbQiHTfpj3zvbw7q4p3uSeRWHHK0ehhHAoYqHyxXwIjmuyGVz3Q00BJL8lkM9',
    environment: 'live'  // CRITICAL: Must be 'live'
};

const BACKEND_CONFIG = {
    baseUrl: 'https://foundation-backend-chi.vercel.app',
    endpoints: {
        createPaymentIntent: '/create-payment-intent',
        subscriptionStatus: '/subscription-status',
        health: '/health'
    }
};
```

### ✅ **Step 3: Copy Payment Processing Functions**
Include these functions exactly as shown in `PAYMENT_TEMPLATE_FOR_NEW_PAGES.html`:

- `initializeStripe()`
- `processPayment()`
- `processDonation()`
- `getUserCurrency()`
- `showError()`
- `showSuccess()`
- `logPaymentSuccess()`

### ✅ **Step 4: Copy HTML Payment Forms**
Copy the modal HTML for:
- Subscription payments (`#subscriptionModal`)
- Donations (`#donationModal`)

---

## 🎯 **Key Integration Points**

### **1. Backend URL (NEVER CHANGE)**
```javascript
// Always use this exact URL:
const response = await fetch('https://foundation-backend-chi.vercel.app/create-payment-intent', {
    method: 'POST',
    headers: { 'Content-Type': 'application/json' },
    body: JSON.stringify({
        planType: selectedPlan,
        currency: userCurrency,
        amount: priceInCents,
        customerEmail: currentUser.email || '',
        customerName: currentUser.displayName || cardholderName
    })
});
```

### **2. Live Environment Check**
```javascript
// Always wrap payment processing in this check:
if (STRIPE_CONFIG.environment === 'live') {
    // Real payment processing here
} else {
    // Test environment fallback
}
```

### **3. Payment Intent Confirmation**
```javascript
// Always confirm payment with Stripe:
const { error: confirmError, paymentIntent } = await stripe.confirmCardPayment(clientSecret, {
    payment_method: paymentMethod.id
});
```

---

## 📂 **File Structure for New Pages**

```
your-new-page.html
├── 📜 HTML Structure
├── 🎨 Your Custom Styles
├── 📝 Your Page Content
├── 💳 Payment Modal HTML (copy from template)
└── 🔧 Payment JavaScript (copy from template)
```

---

## 🔧 **Customization Points**

### **What You CAN Customize:**
- ✅ Page design and layout
- ✅ Custom styling
- ✅ Pricing plans
- ✅ Success/error messages
- ✅ Firebase integration logic
- ✅ Page-specific functionality

### **What You MUST NOT Change:**
- ❌ Backend URL (`https://foundation-backend-chi.vercel.app`)
- ❌ Stripe publishable key
- ❌ Payment processing logic structure
- ❌ Stripe configuration object
- ❌ Backend endpoints

---

## 🚨 **Critical Requirements**

### **1. Stripe Configuration**
```javascript
// This EXACT configuration is required:
const STRIPE_CONFIG = {
    publishableKey: 'pk_live_51Rr5H03QiDHRr52effkP2HrTynAiO7NYD8VQfmbQiHTfpj3zvbw7q4p3uSeRWHHK0ehhHAoYqHyxXwIjmuyGVz3Q00BJL8lkM9',
    environment: 'live'
};
```

### **2. Backend Integration**
```javascript
// Always use the live backend:
const response = await fetch('https://foundation-backend-chi.vercel.app/create-payment-intent', {
    // Payment data
});
```

### **3. Error Handling**
```javascript
// Always include proper error handling:
try {
    // Payment processing
} catch (error) {
    console.error('❌ Payment error:', error);
    showError('paymentError', error.message);
}
```

---

## 📋 **Quick Copy-Paste Sections**

### **Minimal Payment Integration**
For a simple page that just needs payment functionality:

1. Copy the entire `<script>` section from `PAYMENT_TEMPLATE_FOR_NEW_PAGES.html`
2. Copy the payment modal HTML
3. Add buttons to trigger payment modals
4. Done! 🎉

### **Full Integration**
For pages with complete subscription and donation features:

1. Copy everything from the template
2. Customize the styling to match your page
3. Modify pricing plans if needed
4. Add your specific success/error handling

---

## 🧪 **Testing Your Integration**

### **1. Test Payment Flow**
```javascript
// Use Stripe test card:
// Card Number: 4242 4242 4242 4242
// Expiry: Any future date
// CVC: Any 3 digits
```

### **2. Verify Backend Connection**
```javascript
// Check backend health:
fetch('https://foundation-backend-chi.vercel.app/health')
    .then(response => response.json())
    .then(data => console.log('Backend status:', data));
```

### **3. Monitor Console Logs**
Look for these success messages:
- `✅ Stripe initialized successfully`
- `✅ Payment intent created`
- `✅ LIVE payment processed successfully`

---

## 🔄 **Future Updates**

### **If Backend URL Changes:**
1. Update `BACKEND_CONFIG.baseUrl` in all files
2. No other changes needed

### **If Stripe Keys Change:**
1. Update `STRIPE_CONFIG.publishableKey` in all files
2. Update backend environment variables

### **If New Features Added:**
1. Follow this same pattern
2. Always use the backend for payment processing
3. Maintain error handling consistency

---

## 📞 **Need Help?**

If you encounter issues:

1. **Check browser console** for error messages
2. **Verify backend is running:** `https://foundation-backend-chi.vercel.app/health`
3. **Ensure all required scripts are loaded**
4. **Check network tab** for failed API calls

## 🎯 **Success Checklist**

- [ ] Stripe scripts loaded
- [ ] Configuration constants set correctly
- [ ] Payment functions copied
- [ ] HTML modals included
- [ ] Backend URL correct
- [ ] Environment set to 'live'
- [ ] Error handling in place
- [ ] Test payment successful

**Follow this guide for every new page and your payments will work perfectly!** 🚀 