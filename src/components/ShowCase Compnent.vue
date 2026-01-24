<template>
  <div class="showcase-banner">
    <div class="showcase-content">
      <div class="showcase-text">
        <h1>Don't miss amazing grocery deals</h1>
        <p class="showcase-subtitle">Sign up for the daily newsletter</p>

        <div class="newsletter-form">
          <input
            type="email"
            v-model="email"
            placeholder="Your email address"
            class="email-input"
            @keyup.enter="subscribe"
          />
          <button @click="subscribe" class="subscribe-btn" :disabled="!isValidEmail || isSubscribing">
            {{ isSubscribing ? 'Subscribing...' : 'Subscribe' }}
          </button>
        </div>
      </div>

      <div class="showcase-image-container">
        <img
          src="/logo/fresh-apples-shopping-mesh-bag-with-branch-apples-removebg 1.png"
          alt="Fresh Apples"
          class="showcase-image"
        />
      </div>
    </div>

    <div v-if="message" class="message" :class="messageType">
      {{ message }}
    </div>
  </div>
</template>

<script>
export default {
  name: "ShowCaseComponent",
  data() {
    return {
      email: '',
      isSubscribing: false,
      message: '',
      messageType: ''
    };
  },
  computed: {
    isValidEmail() {
      const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
      return emailRegex.test(this.email);
    }
  },
  methods: {
    async subscribe() {
      if (!this.isValidEmail) {
        this.showMessage('Please enter a valid email address', 'error');
        return;
      }

      this.isSubscribing = true;

      try {
        // Simulate API call
        await new Promise(resolve => setTimeout(resolve, 1500));

        this.showMessage('Successfully subscribed! Check your email for confirmation.', 'success');
        this.email = '';
      } catch {
        this.showMessage('Something went wrong. Please try again.', 'error');
      } finally {
        this.isSubscribing = false;
      }
    },

    showMessage(text, type) {
      this.message = text;
      this.messageType = type;

      setTimeout(() => {
        this.message = '';
        this.messageType = '';
      }, 5000);
    }
  }
};
</script>

<style scoped>
.showcase-banner {
  background: linear-gradient(135deg, #fff4dd 0%, #ffe8cc 100%);
  border-radius: 16px;
  padding: 40px;
  margin: 30px 0;
  box-shadow: 0 4px 20px rgba(0, 0, 0, 0.08);
  position: relative;
  overflow: hidden;
}

.showcase-banner::before {
  content: '';
  position: absolute;
  top: -50%;
  right: -10%;
  width: 300px;
  height: 300px;
  background: radial-gradient(circle, rgba(255, 204, 0, 0.1) 0%, transparent 70%);
  border-radius: 50%;
}

.showcase-content {
  display: flex;
  justify-content: space-between;
  align-items: center;
  width: 100%;
  position: relative;
  z-index: 1;
}

.showcase-text {
  flex: 1;
  max-width: 500px;
}

.showcase-text h1 {
  font-size: 48px;
  font-weight: bold;
  color: #333;
  margin: 0 0 16px 0;
  line-height: 1.2;
}

.showcase-subtitle {
  font-size: 18px;
  color: #666;
  margin: 0 0 30px 0;
  line-height: 1.4;
}

.newsletter-form {
  display: flex;
  gap: 0;
  max-width: 400px;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
  border-radius: 8px;
  overflow: hidden;
}

.email-input {
  flex: 1;
  padding: 16px 20px;
  border: none;
  font-size: 16px;
  outline: none;
  background: white;
}

.email-input::placeholder {
  color: #999;
}

.subscribe-btn {
  background: #29a754;
  color: white;
  border: none;
  padding: 16px 24px;
  font-size: 16px;
  font-weight: 600;
  cursor: pointer;
  transition: background 0.3s ease;
  white-space: nowrap;
}

.subscribe-btn:hover:not(:disabled) {
  background: #1e7a3a;
}

.subscribe-btn:disabled {
  background: #ccc;
  cursor: not-allowed;
}

.showcase-image-container {
  flex: 1;
  display: flex;
  justify-content: center;
  align-items: center;
  max-width: 400px;
}

.showcase-image {
  width: 100%;
  max-width: 350px;
  height: auto;
  object-fit: contain;
}


.message {
  position: fixed;
  top: 20px;
  right: 20px;
  padding: 15px 20px;
  border-radius: 8px;
  font-weight: 500;
  z-index: 1000;
}

.message.success {
  background: #d4edda;
  color: #155724;
  border: 1px solid #c3e6cb;
}

.message.error {
  background: #f8d7da;
  color: #721c24;
  border: 1px solid #f5c6cb;
}

@media (max-width: 768px) {
  .showcase-banner {
    padding: 30px 20px;
    margin: 20px 0;
  }

  .showcase-content {
    flex-direction: column;
    text-align: center;
    gap: 30px;
  }

  .showcase-text h1 {
    font-size: 32px;
  }

  .showcase-subtitle {
    font-size: 16px;
  }

  .newsletter-form {
    max-width: 100%;
  }

  .showcase-image-container {
    max-width: 250px;
  }

  .showcase-image {
    max-width: 200px;
  }
}
</style>
