# 🛍️ Bargenix: E-Commerce Bargaining Scenario Generator

This repository provides a modular, extensible system for generating **synthetic negotiation datasets** between a user and a virtual assistant (bot) in an e-commerce setting.

The system captures **negotiation dynamics**, calculating product and user profiles, generating conversation turns, and simulating discount rounds.


## 🔧 Features

- 📊 **Score-Based Decision Logic**: Calculates user and product scores based on behavioral and catalog data.
- 💬 **Dynamic Dialogue Simulation**: Mimics realistic single-turn negotiation between a user and a system.
- 💸 **Discount Round Strategy**: Offers context-aware discounts based on predefined bounds and scores.
- 💾 **JSONL Dataset Export**: Generates clean, structured, and ready-to-train data for LLMs or dialogue systems.
- 🔁 **Supports Multiple Scenarios**: Each scenario includes different rounds, product types, user behaviors, and discount outcomes.


## 📦 Example Output (Single Sample)

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
      ...
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
