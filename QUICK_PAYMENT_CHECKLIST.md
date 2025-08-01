# ⚡ Quick Payment Integration Checklist

## 🚀 **For Every New HTML Page With Payments**

### 📋 **Copy These 4 Things:**

#### 1. **Scripts (Add to `<head>` or before `</body>`)**
```html
<script src="https://js.stripe.com/v3/"></script>
<script src="https://www.gstatic.com/firebasejs/9.0.0/firebase-app-compat.js"></script>
<script src="https://www.gstatic.com/firebasejs/9.0.0/firebase-auth-compat.js"></script>
<script src="https://www.gstatic.com/firebasejs/9.0.0/firebase-firestore-compat.js"></script>
```

#### 2. **Configuration (Copy Exactly)**
```javascript
const STRIPE_CONFIG = {
    publishableKey: 'pk_live_51Rr5H03QiDHRr52effkP2HrTynAiO7NYD8VQfmbQiHTfpj3zvbw7q4p3uSeRWHHK0ehhHAoYqHyxXwIjmuyGVz3Q00BJL8lkM9',
    environment: 'live'
};

const BACKEND_CONFIG = {
    baseUrl: 'https://foundation-backend-chi.vercel.app',
    endpoints: {
        createPaymentIntent: '/create-payment-intent'
    }
};
```

#### 3. **Payment Functions (Copy from `PAYMENT_TEMPLATE_FOR_NEW_PAGES.html`)**
- `initializeStripe()`
- `processPayment()`
- `processDonation()`
- Helper functions

#### 4. **HTML Modals (Copy from template)**
- Subscription modal
- Donation modal

---

## ⚠️ **NEVER CHANGE:**

- ❌ Backend URL: `https://foundation-backend-chi.vercel.app`
- ❌ Stripe publishable key
- ❌ Payment processing structure

---

## ✅ **Test Checklist:**

- [ ] Scripts loaded without errors
- [ ] Configuration copied correctly
- [ ] Payment functions included
- [ ] HTML modals added
- [ ] Test payment works (card: 4242 4242 4242 4242)
- [ ] Console shows: "✅ LIVE payment processed successfully!"

---

## 🔧 **Quick Test:**

```javascript
// Check backend connection:
fetch('https://foundation-backend-chi.vercel.app/health')
    .then(response => response.json())
    .then(data => console.log('✅ Backend working:', data));
```

---

**📁 Files to Reference:**
- `PAYMENT_TEMPLATE_FOR_NEW_PAGES.html` - Complete template
- `NEW_PAGE_PAYMENT_INTEGRATION_GUIDE.md` - Detailed guide

**🎯 Result:** Every new page will have working live payments! 🚀 