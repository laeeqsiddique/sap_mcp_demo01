# 🚀 SAP OData to MCP Bridge - Real-Time Demo
**Built by [Cremencing Solutions](https://www.linkedin.com/company/cremencing-solutions)**

> Transform SAP enterprise data into AI-ready conversational interfaces using the Model Context Protocol (MCP). This project demonstrates real-time integration between SAP S/4HANA and modern AI applications.

[![GitHub Stars](https://img.shields.io/github/stars/yourusername/sap-mcp-bridge?style=social)](https://github.com/yourusername/sap-mcp-bridge)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-Cremencing%20Solutions-blue)](https://www.linkedin.com/company/cremencing-solutions)
[![SAP](https://img.shields.io/badge/SAP-API%20Hub-orange)](https://api.sap.com)

## ⭐ Please Star This Repository!
If you find this project helpful, please give it a star! It helps others discover this resource and motivates us to keep improving it.

## 🎯 What This Project Does

This demo showcases a complete integration between SAP's Business Partner API and modern AI interfaces through MCP (Model Context Protocol). It provides:

- **Real SAP Data**: Live connection to SAP API Hub sandbox
- **OData Filtering**: Demonstrates real `$filter`, `$top`, `$select` capabilities
- **Modern UI**: Beautiful React/Next.js interface
- **MCP Integration**: Ready for AI-powered conversations
- **Production Ready**: Deploy to Railway, Vercel, or SAP BTP

## 📺 Live Demo

Watch the demo in action:
- 🔴 Live filtering of Business Partners
- 🔴 Real-time SAP data retrieval
- 🔴 Category-based filtering (Customers vs Suppliers)
- 🔴 Beautiful UI with instant responses

## 🏗️ Architecture

```
┌─────────────┐    ┌─────────────┐    ┌─────────────┐    ┌─────────────┐
│   Next.js   │───▶│ MCP Server  │───▶│  SAP API    │───▶│ S/4HANA     │
│   Frontend  │    │  (Bridge)   │    │    Hub      │    │   System    │
└─────────────┘    └─────────────┘    └─────────────┘    └─────────────┘
   localhost:3009    localhost:3335    api.sap.com        SAP Cloud
```

## 🚀 Quick Start (5 Minutes)

### Prerequisites
- Node.js 18+ installed
- Git installed
- Web browser (Chrome/Firefox/Edge)

### Step 1: Clone the Repository

```bash
git clone https://github.com/yourusername/sap-mcp-bridge.git
cd sap-mcp-bridge
```

### Step 2: Get Your SAP API Key (Free)

1. **Visit SAP API Business Hub**
   - Go to [https://api.sap.com](https://api.sap.com)
   - Click "Login" in the top right corner

2. **Create a Free Account**
   - Click "Sign Up" if you don't have an account
   - Fill in your details
   - Verify your email

3. **Get Your API Key**
   - Once logged in, click on your profile icon
   - Select "Settings" or "Preferences"
   - Find the "Show API Key" button
   - Copy your API key (looks like: `QLsJHC4xbqjJXsCbDQCjhhB6qtIsnAB5`)

4. **Test Your API Key**
   - Go to [Business Partner API](https://api.sap.com/api/API_BUSINESS_PARTNER/tryout)
   - Click "Try Out"
   - Your API key should auto-populate
   - Click "Execute" to test

### Step 3: Setup Backend (MCP Server)

```bash
# Navigate to backend
cd btp-sap-odata-to-mcp-server

# Install dependencies
npm install

# Create environment file
cp .env.example .env

# Edit .env file and add your API key
# Open .env in any text editor and update:
# SAP_APIHUB_APIKEY=your_api_key_here
```

**Windows Users:**
```powershell
# Use notepad to edit
notepad .env
```

**Mac/Linux Users:**
```bash
# Use nano or vim
nano .env
```

### Step 4: Build and Start Backend

```bash
# Build the TypeScript project
npm run build

# Start the MCP server
npm run start:local
```

You should see:
```
🚀 Local SAP MCP Server running at http://0.0.0.0:3333
📊 Health check: http://localhost:3333/health
🔧 MCP endpoint: http://localhost:3333/mcp
```

**Keep this terminal running!**

### Step 5: Setup Frontend (Next.js App)

Open a **new terminal** and:

```bash
# Navigate to frontend from project root
cd ../sap-mcp-demo

# Install dependencies
npm install

# Start the development server
npm run dev
```

You should see:
```
▲ Next.js 15.5.3
- Local: http://localhost:3000
✓ Ready
```

### Step 6: Test the Demo

1. Open your browser to [http://localhost:3000](http://localhost:3000)
2. Try these queries in the chat interface:
   - "List 5 business partners"
   - "Show me suppliers"
   - "Search for customers"
   - "Get business partner addresses"

## 📋 Detailed Setup Instructions

### Environment Variables Explained

Create a `.env` file in `btp-sap-odata-to-mcp-server` directory:

```bash
# Server Configuration
PORT=3333                    # Port for MCP server
ALLOWED_ORIGINS=*           # CORS settings

# SAP API Hub Configuration
SAP_ODATA_BASE=https://sandbox.api.sap.com/s4hanacloud/sap/opu/odata/sap/API_BUSINESS_PARTNER
SAP_APIHUB_APIKEY=your_api_key_here  # YOUR API KEY HERE!

# MCP Configuration
MCP_TOOL_REGISTRY_TYPE=hierarchical
LOG_LEVEL=info
LOCAL_MODE=true
```

### Testing the Backend

Test if your backend is working:

```bash
# Test health endpoint
curl http://localhost:3333/health

# Test business partners endpoint
curl "http://localhost:3333/api/business-partners?top=2"

# Test suppliers endpoint
curl "http://localhost:3333/api/suppliers?category=2"
```

## 🎮 Features Demonstration

### 1. Real OData Filtering
The backend implements real SAP OData filtering:

```javascript
// Category filtering for suppliers
$filter=BusinessPartnerCategory eq '2'

// Category filtering for customers
$filter=BusinessPartnerCategory eq '1'

// Limit results
$top=5
```

### 2. Available Endpoints

| Endpoint | Description | Example |
|----------|-------------|---------|
| `/api/business-partners` | List all partners | `?top=5&category=1` |
| `/api/suppliers` | List suppliers | `?top=5&category=2` |
| `/api/addresses` | Partner addresses | `?top=5` |
| `/api/business-partner/:id` | Get specific partner | `/api/business-partner/11` |

### 3. Frontend Query Processing
The frontend intelligently processes natural language:

- "suppliers" → Filters with `category=2`
- "customers" → Filters with `category=1`
- "5 partners" → Sets `top=5`

## 🚀 Deployment

### Deploy to Railway (Recommended)

1. **Push to GitHub**
```bash
git add .
git commit -m "Initial deployment"
git push origin main
```

2. **Deploy on Railway**
- Go to [Railway.app](https://railway.app)
- Click "New Project" → "Deploy from GitHub"
- Select your repository
- Add environment variable: `SAP_APIHUB_APIKEY`
- Click "Deploy"

### Deploy to Vercel

Frontend only:
```bash
cd sap-mcp-demo
npx vercel
```

### Deploy to SAP BTP

See [BTP Deployment Guide](./docs/BTP_DEPLOYMENT.md)

## 🛠️ Troubleshooting

### Common Issues

**1. Port Already in Use**
```bash
# Kill process on port 3333
# Windows
netstat -ano | findstr :3333
taskkill /PID <PID> /F

# Mac/Linux
lsof -i :3333
kill -9 <PID>
```

**2. API Key Not Working**
- Verify key at [api.sap.com](https://api.sap.com)
- Check for extra spaces in .env file
- Ensure key is inside quotes if it contains special characters

**3. No Data Returned**
- Check backend logs for errors
- Verify SAP API Hub is accessible
- Test API key directly on SAP API Hub website

**4. Frontend Can't Connect to Backend**
- Ensure backend is running on port 3333
- Check CORS settings in backend
- Try accessing backend health endpoint directly

## 📊 Understanding the Demo

### What Makes This Special?

1. **Real SAP Data**: Unlike mock demos, this connects to actual SAP systems
2. **Production Patterns**: Implements real-world filtering and error handling
3. **Modern Stack**: Uses latest Next.js, TypeScript, and MCP protocols
4. **Extensible**: Easy to add more SAP services and entities

### Key Learning Points

- How to integrate SAP OData services with modern web apps
- Implementing MCP protocol for AI integration
- Building proxy servers to handle API keys securely
- Real-time data filtering with OData syntax

## 🤝 Contributing

We welcome contributions! Please:

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Submit a pull request

## 💼 About Cremencing Solutions

**[Cremencing Solutions](https://www.linkedin.com/company/cremencing-solutions)** specializes in SAP integrations and modern cloud architectures. We help enterprises bridge the gap between traditional SAP systems and modern AI/cloud technologies.

### Our Services
- SAP Integration Consulting
- Cloud Migration (SAP BTP, AWS, Azure)
- Custom MCP Development
- AI/ML Integration with SAP

### Contact Us
- LinkedIn: [Cremencing Solutions](https://www.linkedin.com/company/cremencing-solutions)
- Email: contact@cremencing.com
- Website: [www.cremencing.com](https://www.cremencing.com)

## 📚 Resources

- [SAP API Business Hub](https://api.sap.com)
- [Model Context Protocol Docs](https://modelcontextprotocol.io)
- [OData Documentation](https://www.odata.org)
- [Next.js Documentation](https://nextjs.org/docs)

## 🙏 Acknowledgments

This project was inspired by the original [btp-sap-odata-to-mcp-server](https://github.com/lemaiwo/btp-sap-odata-to-mcp-server) by lemaiwo. We've extended it with real-time filtering, modern UI, and production-ready features.

## 📄 License

MIT License - See [LICENSE](LICENSE) for details

---

## ⭐ Don't Forget to Star!

If this project helped you, please star it on GitHub! It helps others find this resource and motivates us to create more open-source SAP integration tools.

**Built with ❤️ by [Cremencing Solutions](https://www.linkedin.com/company/cremencing-solutions)**

---

### Need Help?

- 📧 Reach out on [LinkedIn](https://www.linkedin.com/company/cremencing-solutions)
- 🐛 Report issues on [GitHub Issues](https://github.com/yourusername/sap-mcp-bridge/issues)
- 💡 Request features via [GitHub Discussions](https://github.com/yourusername/sap-mcp-bridge/discussions)

### Quick Links

- [Get SAP API Key](https://api.sap.com)
- [Deploy to Railway](https://railway.app)
- [Contact Cremencing Solutions](https://www.linkedin.com/company/cremencing-solutions)