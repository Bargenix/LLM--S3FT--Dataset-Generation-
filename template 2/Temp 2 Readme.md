# 🛍️ Bargenix: E-Commerce Bargaining Scenario Generator Template 2

This repository provides a modular, extensible system for generating **synthetic negotiation datasets** between a user and a virtual assistant (bot) in an e-commerce setting.

The system captures **negotiation dynamics**, calculating product and user profiles, generating conversation turns, and simulating discount rounds.


## 🔧 Features

- 📊 **Score-Based Decision Logic**: Calculates user and product scores based on behavioral and catalog data.
- 💬 **Dynamic Dialogue Simulation**: Mimics realistic single-turn negotiation between a user and a system.
- 💸 **Discount Round Strategy**: Offers context-aware discounts based on predefined bounds and scores.
- 💾 **JSONL Dataset Export**: Generates clean, structured, and ready-to-train data for LLMs or dialogue systems.
- 🔁 **Supports Multiple Scenarios**: Each scenario includes different rounds, product types, user behaviors, and discount outcomes.


## 📦 Example Output (Single Sample)
### 🧾 Standard Turn (Mid-Negotiation)
```json
{
  "Live_data_from_frontend": "User Info:\nuser_name = Shanaya, email = shanaya@gmail.com, ...\n\nProduct Info:\nproduct_name = Electric Fan, ...",
  "user": "User: 19% is less it seems is that all you can offer,ok lets say if you can make it to 31 thats a deal",
  "response": "Bot: Thats quite a high ask at 31%. But since you've come this far, I can drop the price to 1070.45 INR, which gives you 21% off.",
  "metadata": {
    "user_email_id": "shanaya@gmail.com",
    "user_score": 25.45,
    "bargain_score": 69,
    "product_score": 16.35,
    "admin_max_discount_from_min_price": 44,
    "system_max_discount": 23,
    "max_round_count": 6,
    "current_round": 5,
    "previous_round_discount_given": 19,
    "user_req": 31,
    "current_discount": 21,
    "current_discount_price": 1070.45,
    "round_discounts": {
      "round_count1": 9,
      "round_count2": 13,
      "round_count3": 17,
    }
  }
}
```
### ✅ Final Round Turn (End-of-Negotiation Scenario)
If the current_round equals the max_round_count, Bargenix attempts to close the negotiation with a final offer:
```json
{
  "Live_data_from_frontend": "User Info:\nuser_name = Meera, email = meera@gmail.com, orders = 12, spent = 5014, email_verified = meera@gmail.com, refunds = 514, days_since_last = 60\n\nProduct Info:\nproduct_name = Headband, product_description = Stretchable headband, perfect for workouts or casual wear., product_color = Emerald, product_size = One Size, product_price = 4664 INR, min_price_client = 2006 INR, avg_inventory = 65, product_tag = electronics, product_type = seasonal, images_count = 2, days_since_creation = 37\n\n",
  "user": "User: 30% is less it seems is that all you can offer,ok lets say if you can make it to 58 thats a deal",
  "response": "Bot: thats way much higher at 58%. Since you’ve come this far, I can lower the price from my side—how about 3124.88 INR, which is up to 33% off. This is my final offer and a compact deal I can get you now itself.",
  "metadata": {
    "user_email_id": "meera@gmail.com",
    "user_score": 32.15,
    "bargain_score": 41,
    "product_price": 4664,
    "product_score": 20.52,
    "admin_max_discount_from_min_price": 57,
    "system_max_discount": 33,
    "max_round_count": 6,
    "current_round": 6,
    "previous_round_discount_given": 30,
    "user_req": 58,
    "current_discount": 33,
    "current_discount_price": 3124.88,
    "round_discounts": {
      "round_count1": 13,
      "round_count2": 20,
      "round_count3": 24,
      "round_count4": 27,
      "round_count5": 30,
      "round_count6": 33
    }
  }
}

```

## 🧠 Core Concepts

### User Score
Evaluates the user’s profile based on:
- Number of orders
- Total spend vs refunds
- Recency of last purchase
- Email verification status

### Product Score
Determined by:
- Product age
- Inventory levels
- Number of images
- Type (seasonal or regular)
- Tags (e.g., summer, winter)
- Average price

### Bargain Score
A randomized score (30–100) representing how aggressive the bargain is.

## 🔁 Negotiation Dynamics:

### 🔻 Max Rounds
The number of negotiation rounds is dynamically calculated based on:
- User Score
- Product Score
- Bargain Score

### 📂 Explore the full code and datasets on GitHub
[🔗 Bargenix GitHub Repository](https://github.com/Bargenix/fastapi_llm_backend/blob/2da7d87a4537cf7202238e83f2f98a76306de75c/helper.py)

## 🔥 Lower Bound
Used to define a minimum threshold for rounds, focusing on later turns (typically rounds 3 to 6) where negotiations intensify. These rounds often yield more informative samples for LLM fine-tuning.

## Discount System
- Admin Max Discount: Randomly chosen per product.
- System Max Discount: Adjusted based on product, user, and bargain score.
- Round-Wise Discounts: Logarithmic progression of discounts across rounds.

## 🧪 How to Generate Data
You can generate bargaining scenarios either saved to a file or in-memory for quick experimentation.

### Generate to File (JSONL Format)
Generate 50 independent bargaining scenarios, each representing a single negotiation turn, and save them as a JSON Lines file:
```bash
generate_dataset(n=50, filename="bargenix_dataset.jsonl")
```

### 🧪 Generate In-Memory (for Jupyter or Debugging)
Generate 5 scenarios directly in memory (without saving to file):
```bash
data = n_generate_datasets(n=5)
```
## Each generated scenario simulates a full bargaining turn, including:
- Product metadata
- User behavior
- Dynamic pricing
- User request and bot counter-offer
