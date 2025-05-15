<template>
  <Teleport to="body">
    <!-- Modal Backdrop -->
    <div
      v-if="isOpen"
      class="modal-backdrop"
      @click="closeModal"
    >
      <!-- Modal Content -->
      <div
        class="modal-content"
        :class="{ 'modal-open': isOpen }"
        @click.stop
      >
        <!-- Modal Header -->
        <div class="modal-header">
          <h3 class="modal-title">Please fill in your information</h3>
          <button
            @click="closeModal"
            class="modal-close-btn"
            aria-label="Close"
          >
            <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
              <line x1="18" y1="6" x2="6" y2="18"></line>
              <line x1="6" y1="6" x2="18" y2="18"></line>
            </svg>
          </button>
        </div>

        <!-- Modal Body -->
        <div class="modal-body">
          <!-- Donation Type Toggle -->
          <div class="donation-toggle">
            <div class="toggle-options">
              <span :class="{ 'active': isDonationMonthly }">Monthly</span>
              <label class="toggle-switch">
                <input type="checkbox" v-model="isDonationMonthly" />
                <span class="toggle-slider"></span>
              </label>
              <span :class="{ 'active': !isDonationMonthly }">One-off</span>
            </div>
            <div class="amount-display">
              <span>PHP</span>
              <input
                type="number"
                v-model.number="donationAmount"
                min="1"
                @input="validateAmount"
              />
            </div>
          </div>

          <form @submit.prevent="submitDonation">
            <!-- Name Fields -->
            <div class="form-row">
              <div class="form-group">
                <label for="firstName">First Name</label>
                <input
                  id="firstName"
                  v-model="formData.firstName"
                  type="text"
                  placeholder="First Name"
                  required
                />
              </div>
              <div class="form-group">
                <label for="lastName">Last Name</label>
                <input
                  id="lastName"
                  v-model="formData.lastName"
                  type="text"
                  placeholder="Last Name"
                  required
                />
              </div>
            </div>

            <!-- Email Field -->
            <div class="form-group">
              <label for="email">Email</label>
              <input
                id="email"
                v-model="formData.email"
                type="email"
                placeholder="Email"
                required
              />
            </div>

            <!-- Mobile Number Field -->
            <div class="form-group">
              <label for="mobile">Mobile No.</label>
              <input
                id="mobile"
                v-model="formData.mobile"
                type="tel"
                placeholder="0__ ___ ____ (PH only)"
                pattern="0[0-9]{2}[0-9]{3}[0-9]{4}"
                required
              />
            </div>

            <!-- Card Number Field -->
            <div class="form-group">
              <label for="cardNumber">
                Card Number
                <span class="card-icons">
                  <img src="./icons/c1.png" alt="Visa" />
                  <img src="./icons/c2.png" alt="Mastercard" />
                  <img src="./icons/c3.png" alt="JCB" />
                  <img src="./icons/c4.png" alt="American Express" />
                </span>
              </label>
              <input
                id="cardNumber"
                v-model="formData.cardNumber"
                type="text"
                placeholder="____ ____ ____ ____"
                maxlength="19"
                @input="formatCardNumber"
                required
              />
            </div>

            <!-- Expiry Date and CVV Fields -->
            <div class="form-row">
              <div class="form-group">
                <label for="expiryDate">Expiry date</label>
                <input
                  id="expiryDate"
                  v-model="formData.expiryDate"
                  type="text"
                  placeholder="MM/YY or YYYY"
                  maxlength="7"
                  @input="formatExpiryDate"
                  required
                />
              </div>
              <div class="form-group">
                <label for="cvv">CVV</label>
                <input
                  id="cvv"
                  v-model="formData.cvv"
                  type="text"
                  placeholder="3-4 digit"
                  maxlength="4"
                  pattern="[0-9]{3,4}"
                  required
                />
              </div>
            </div>

            <!-- Consent Checkbox -->
            <div class="form-group checkbox-group">
              <label>
                <input
                  type="checkbox"
                  v-model="formData.receiveUpdates"
                />
                <span>
                  Yes! Please send me important updates from Aboitiz Foundation.
                  Aboitiz Foundation respects and protects your personal information and you can
                  unsubscribe at any time. For more details please refer to Aboitiz Foundation privacy policy
                </span>
              </label>
            </div>

            <!-- Submit Button -->
            <button
              type="submit"
              class="donate-button"
            >
              DONATE NOW
            </button>
          </form>



        </div>
      </div>
    </div>
  </Teleport>
</template>

<script setup lang="ts">
import { ref, defineEmits, defineProps, watch } from 'vue';

const props = defineProps({
  isOpen: {
    type: Boolean,
    default: false
  }
});

const emit = defineEmits(['close', 'editAmount', 'submit']);

const isDonationMonthly = ref(true);
const donationAmount = ref(800);

const formData = ref({
  firstName: '',
  lastName: '',
  email: '',
  mobile: '',
  cardNumber: '',
  expiryDate: '',
  cvv: '',
  receiveUpdates: true
});

// Close modal when clicking outside
const closeModal = () => {
  emit('close');
};

// Format card number with spaces
const formatCardNumber = (event: Event) => {
  const input = event.target as HTMLInputElement;
  let value = input.value.replace(/\s+/g, '').replace(/[^0-9]/gi, '');

  const parts = [];
  for (let i = 0; i < value.length; i += 4) {
    parts.push(value.substring(i, i + 4));
  }

  formData.value.cardNumber = parts.join(' ');
};

// Format expiry date
const formatExpiryDate = (event: Event) => {
  const input = event.target as HTMLInputElement;
  let value = input.value.replace(/\s+/g, '').replace(/[^0-9]/gi, '');

  if (value.length > 2) {
    formData.value.expiryDate = value.substring(0, 2) + '/' + value.substring(2);
  } else {
    formData.value.expiryDate = value;
  }
};

// Validate donation amount
const validateAmount = () => {
  // Ensure amount is a positive number
  if (donationAmount.value <= 0 || isNaN(donationAmount.value)) {
    donationAmount.value = 100; // Default to 100 if invalid
  }

  // Round to whole number
  donationAmount.value = Math.round(donationAmount.value);
};

// Edit amount function
const editAmount = () => {
  // Find the donation amount input and focus it
  const amountInput = document.querySelector('.amount-display input');
  if (amountInput) {
    (amountInput as HTMLInputElement).focus();
    (amountInput as HTMLInputElement).select();
  }
};

// Submit donation
const submitDonation = () => {
  emit('submit', {
    ...formData.value,
    amount: donationAmount.value,
    isMonthly: isDonationMonthly.value
  });
};

// Close modal when escape key is pressed
watch(
  () => props.isOpen,
  (isOpen) => {
    if (isOpen) {
      document.body.style.overflow = 'hidden'; // Prevent scrolling when modal is open

      const handleEscape = (e: KeyboardEvent) => {
        if (e.key === 'Escape') {
          closeModal();
        }
      };

      document.addEventListener('keydown', handleEscape);

      return () => {
        document.removeEventListener('keydown', handleEscape);
        document.body.style.overflow = ''; // Restore scrolling when modal is closed
      };
    }
  },
  { immediate: true }
);
</script>

<style scoped>
/* Modal Styles */
.modal-backdrop {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background-color: rgba(0, 0, 0, 0.5);
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 9999; /* Very high z-index to ensure it's on top */
  padding: 1rem;
}

.modal-content {
  background-color: white;
  border-radius: 0.5rem;
  box-shadow: 0 10px 25px rgba(0, 0, 0, 0.2);
  width: 100%;
  max-width: 500px;
  max-height: 90vh;
  overflow-y: auto;
  transform: scale(0.95);
  opacity: 0;
  transition: transform 0.3s ease, opacity 0.3s ease;
}

.modal-open {
  transform: scale(1);
  opacity: 1;
}

.modal-header {
  position: relative;
  padding: 1.25rem;
  border-bottom: 1px solid #e5e7eb;
}

.modal-title {
  font-size: 1.25rem;
  font-weight: 600;
  color: #374151;
  margin: 0;
}

.modal-close-btn {
  position: absolute;
  top: 1rem;
  right: 1rem;
  background: none;
  border: none;
  color: #6b7280;
  cursor: pointer;
  padding: 0.25rem;
  transition: color 0.2s ease;
}

.modal-close-btn:hover {
  color: #111827;
}

.modal-body {
  padding: 1.25rem;
}

/* Donation Toggle Styles */
.donation-toggle {
  display: flex;
  align-items: center;
  justify-content: space-between;
  background-color: rgba(220, 27, 40, 0.1);
  border-radius: 0.375rem;
  padding: 0.5rem 1rem;
  margin-bottom: 1.5rem;
}

.toggle-options {
  display: flex;
  align-items: center;
  gap: 0.5rem;
}

.toggle-options span {
  font-weight: 500;
  color: #4b5563;
}

.toggle-options span.active {
  color: #dc1b28;
}

.toggle-switch {
  position: relative;
  display: inline-block;
  width: 48px;
  height: 24px;
}

.toggle-switch input {
  opacity: 0;
  width: 0;
  height: 0;
}

.toggle-slider {
  position: absolute;
  cursor: pointer;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background-color: #e5e7eb;
  transition: 0.4s;
  border-radius: 24px;
}

.toggle-slider:before {
  position: absolute;
  content: "";
  height: 18px;
  width: 18px;
  left: 3px;
  bottom: 3px;
  background-color: white;
  transition: 0.4s;
  border-radius: 50%;
}

input:checked + .toggle-slider {
  background-color: #dc1b28;
}

input:checked + .toggle-slider:before {
  transform: translateX(24px);
}

.amount-display {
  display: flex;
  align-items: center;
}

.amount-display span {
  color: #dc1b28;
  font-weight: 500;
  margin-right: 0.25rem;
}

.amount-display input {
  background-color: #dc1b28;
  color: white;
  border: none;
  border-radius: 0.25rem;
  padding: 0.25rem 0.5rem;
  width: 80px;
  text-align: center;
  font-weight: 500;
}

.amount-display input:focus {
  outline: none;
  box-shadow: 0 0 0 2px rgba(220, 27, 40, 0.5);
}

/* Form Styles */
.form-row {
  display: grid;
  grid-template-columns: 1fr;
  gap: 1rem;
  margin-bottom: 1rem;
}

@media (min-width: 640px) {
  .form-row {
    grid-template-columns: 1fr 1fr;
  }
}

.form-group {
  margin-bottom: 1rem;
}

.form-group label {
  display: block;
  color: #4b5563;
  margin-bottom: 0.25rem;
}

.form-group input[type="text"],
.form-group input[type="email"],
.form-group input[type="tel"] {
  width: 100%;
  padding: 0.5rem 0.75rem;
  border: 1px solid #d1d5db;
  border-radius: 0.375rem;
  transition: border-color 0.2s ease, box-shadow 0.2s ease;
}

.form-group input:focus {
  outline: none;
  border-color: #dc1b28;
  box-shadow: 0 0 0 2px rgba(220, 27, 40, 0.25);
}

.card-icons {
  display: inline-flex;
  gap: 0.25rem;
  margin-left: 0.5rem;
}

.card-icons img {
  height: 24px;
  width: auto;
}

.checkbox-group label {
  display: flex;
  align-items: flex-start;
}

.checkbox-group input[type="checkbox"] {
  margin-top: 0.25rem;
  margin-right: 0.5rem;
}

.checkbox-group span {
  font-size: 0.875rem;
  color: #6b7280;
}

.donate-button {
  width: 100%;
  background-color: #dc1b28;
  color: white;
  font-weight: 700;
  padding: 0.75rem 1rem;
  border: none;
  border-radius: 0.375rem;
  cursor: pointer;
  transition: background-color 0.2s ease;
}

.donate-button:hover {
  background-color: #c01824;
}

.edit-amount {
  margin-top: 1rem;
  text-align: center;
}

.edit-amount button {
  display: inline-flex;
  align-items: center;
  color: #6b7280;
  background: none;
  border: none;
  cursor: pointer;
  transition: color 0.2s ease;
}

.edit-amount button svg {
  margin-right: 0.25rem;
}

.edit-amount button:hover {
  color: #dc1b28;
}
</style>
