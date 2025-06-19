# Willys Agent Meal Planner

An intelligent meal planning agent that integrates with Cursor to create personalized weekly meal plans using real-time data from Sweden's Willys grocery store chain.

## 🎯 What It Does

This project combines AI-powered meal planning with live grocery data to create the ultimate Swedish meal planning experience. Using Cursor's agent mode, it can understand your preferences, search Willys for current prices and availability, and generate complete meal plans with shopping lists.

## ✨ Key Features

- 🤖 **AI-Powered Planning**: Natural language meal planning through Cursor agent
- 🛒 **Real-Time Pricing**: Live integration with Willys.se API for current prices
- 🍽️ **Smart Meal Variety**: Balanced nutrition and varied cuisine suggestions
- 💰 **Budget Optimization**: Meal plans that respect your grocery budget
- 📱 **Swedish Language Support**: Proper handling of Swedish product names and characters
- 🏷️ **Dietary Filters**: Support for vegetarian, gluten-free, lactose-free, and more
- 📝 **Beautiful Output**: Formatted markdown meal plans and shopping lists

## 🚀 How It Works

### With Cursor Agent Mode:

1. **Tell the agent your preferences**: "Plan meals for 4 people, 800 kr budget, vegetarian"
2. **Agent searches Willys in real-time**: Finds ingredients, prices, and deals
3. **Generates complete meal plan**: Balanced weekly schedule with recipes
4. **Creates shopping list**: Organized by store sections with current prices
5. **Provides meal prep tips**: Optimization suggestions for efficient cooking

### Example Agent Conversation:

```
You: "I need a week of meals for 2 people, budget 600 kr, prefer quick meals"

Agent: "Let me search Willys for the best deals this week...
Found great prices on chicken (15% off) and seasonal vegetables.
I'll focus on 30-minute meals and include 2 slow-cooker options for variety.

Here's your complete meal plan: [generates detailed plan]
Total cost: 580 kr (under budget!)
Shopping list organized by store sections attached."
```

## 🔗 Documentation

- **[Agent Concept](AGENT_CONCEPT.md)** - Detailed explanation of agent capabilities and workflows
- **[Willys API Documentation](WILLYS_API.md)** - Complete reverse-engineered API reference
- **[Meal Plan Template](meal-plan-template.md)** - Example of generated meal plan format

## 🎯 Use Cases

### **Family Meal Planning**

- Weekly meal prep for busy families
- Budget-conscious grocery shopping
- Dietary restriction accommodation
- Seasonal ingredient optimization

### **Individual Planning**

- Quick weeknight meals for professionals
- Healthy eating goal support
- Cost-effective single-person portions
- Cooking skill development

### **Special Occasions**

- Holiday meal planning
- Dinner party preparation
- Seasonal celebration menus
- Guest dietary accommodation

## 🛠️ Technical Foundation

Built on solid reverse-engineered API knowledge:

- Complete Willys.se search API integration
- Product detail API for nutritional data
- Swedish character encoding support
- Real-time price and availability checking
- Promotional deal detection

## 📄 License

Open source - feel free to adapt for other grocery store APIs or regions!
