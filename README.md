# 🏠 Vassell Household Finance & Governance

A comprehensive planning and budgeting app designed specifically for multi-adult families (3-5 adults plus children) who want to implement fair cost sharing, care work compensation, and structured governance.

## 🌟 Core Features

### **Fair Cost Sharing with Unit Method**
- **Adult Units**: Each adult contributes 1.0 unit
- **Child Units**: Configurable weight (default 0.6) per child
- **Income Caps**: Maximum percentage of net income for Core contributions (5%-60%)
- **Automatic Rebalancing**: Intelligent adjustment when caps are hit
- **Override Support**: Manual adjustments when needed

### **Care Work Compensation**
- **Credit Model**: Care work reduces next month's Core share
- **Stipend Model**: Care work paid from Core budget
- **Configurable Rate**: Set hourly compensation rate
- **Audit Trail**: Track all care entries with timestamps

### **Vision & Buffers Planning**
- **Emergency Fund**: Target based on months of Core expenses
- **Sinking Funds**: Annual targets for major expenses
- **Priority System**: Automatic prioritization of funds
- **Monthly Transfers**: Calculated contribution amounts

### **Governance & Decision Making**
- **Monthly Councils**: Structured 60-minute meetings
- **Voting System**: Configurable quorum requirements
- **Decision Tracking**: Log all decisions and amendments
- **Large Purchase Policy**: Threshold-based approval requirements

## 🚀 Getting Started

### Prerequisites
- Node.js 18.0.0 or higher
- npm or yarn package manager

### Installation

1. **Clone or download the project**
   ```bash
   cd vassell-finance-app
   ```

2. **Install dependencies**
   ```bash
   npm install
   ```

3. **Start the application**
   ```bash
   npm start
   ```

4. **Open your browser**
   Navigate to `http://localhost:3000`

### Development Mode
```bash
npm run dev
```

## 📋 Onboarding Process

### 1. Household Basics
- **Name**: Your household identifier
- **Currency**: Primary currency for all calculations
- **Adults**: 3-5 adult members with names and net incomes
- **Children**: Count and unit weight for cost sharing

### 2. Financial Settings
- **Income Cap**: Maximum percentage of income for Core (5%-60%)
- **Care Model**: Choose between credit or stipend approach
- **Care Rate**: Hourly compensation for care work
- **Vision Allocation**: Percentage for long-term goals (0%-50%)

### 3. Emergency & Sinking Funds
- **Emergency Months**: Target months of Core expenses
- **Sinking Funds**: JSON array of annual targets and accounts

### 4. Governance
- **Quorum Requirements**: For routine and major decisions
- **Purchase Thresholds**: Automatic approval levels

## 💰 How the Unit Method Works

### Basic Calculation
```
totalUnits = numberAdults × 1.0 + totalChildUnits
unitCost = coreTotal / totalUnits
prelimShare[i] = unitCost × (1.0 + assignedChildUnits[i])
```

### Income Caps
```
capAmount[i] = capPercent × netIncome[i]
finalShare[i] = MIN(prelimShare[i], capAmount[i])
```

### Rebalancing
When caps create imbalances, the system automatically rebalances across uncapped adults proportionally until the difference from Core total is within $0.01.

### Example
- **3 adults, 4 children** with childUnitWeight = 0.6
- **Total units**: 3 + (4 × 0.6) = 5.4
- **Core total**: $6,000
- **Unit cost**: $6,000 ÷ 5.4 = $1,111.11
- **Each adult gets**: 1.0 + 1.2 = 2.2 units
- **Preliminary share**: $1,111.11 × 2.2 = $2,444.44

## 🔄 Monthly Workflow

### 1. **Period Setup**
- Set Core total for the month
- Assign child units (must balance to zero)
- Set optional overrides

### 2. **Calculation**
- Run unit method with caps and rebalancing
- Apply care ledger (credits or stipends)
- Plan vision and buffer allocations

### 3. **Review & Adjust**
- Review all calculations and warnings
- Adjust parameters if needed
- Validate child unit assignments

### 4. **Close Month**
- Lock period to prevent changes
- Generate council agenda
- Export all documents and data

## 📊 Care Ledger Models

### Credit Model
- Care work hours × hourly rate = credit amount
- Credit reduces next month's Core contribution
- Example: 10 hours × $20/hour = $200 credit

### Stipend Model
- Care work hours × hourly rate = stipend payment
- Stipend paid from Core budget
- Increases next month's Core total

## 🎯 Vision & Buffers

### Emergency Fund
- Target: `emergencyMonths × monthlyCore`
- Status tracking: building, maintaining, fully funded
- Priority: Highest

### Sinking Funds
- **Priority 1**: Emergency-related (medical, deductibles)
- **Priority 2**: Home and vehicle maintenance
- **Priority 3**: Other goals and expenses

### Monthly Transfers
- Calculated as `annualTarget ÷ 12`
- Automatic prioritization
- Balance checking against vision allocation

## 🏛️ Governance System

### Council Meetings
- **Duration**: 60 minutes monthly
- **Agenda**: 7 structured sections
- **Minutes**: Template with action items
- **Calendar**: ICS file for scheduling

### Decision Making
- **Routine**: Simple majority with routine quorum
- **Major**: Higher quorum requirements
- **Large Purchases**: Threshold-based approval
- **Unanimous**: Required for high-value items

### Voting Members
- All listed adults are voting members
- Quorum requirements are configurable
- Decision logging with timestamps

## 📁 Data Export

### Available Formats
- **Charter Document**: DOCX with styling
- **Calculator Sheet**: Excel with formulas
- **Council Calendar**: ICS file
- **CSV Files**: Decisions, amendments, minutes
- **JSON Export**: Complete household data

### Export Timing
- **Onboarding**: Initial charter and calculator
- **Monthly Close**: All period documents
- **On Demand**: Current household configuration

## 🔧 Technical Architecture

### Backend
- **Node.js/Express**: RESTful API server
- **ES6 Modules**: Modern JavaScript structure
- **In-Memory Storage**: For development (production: database)
- **Validation**: Comprehensive input validation

### Frontend
- **Vanilla JavaScript**: No framework dependencies
- **Responsive Design**: Works on all devices
- **Real-time Validation**: Immediate feedback
- **Progressive Enhancement**: Core functionality first

### Data Models
- **Household**: Configuration and settings
- **Period**: Monthly financial data
- **Calculators**: Business logic engines
- **Exporters**: Document generation

## 🧪 Testing the System

### Test Case
The system includes a built-in test case:
- **3 adults** with incomes [$4,500, $3,200, $2,800]
- **4 children** with childUnitWeight = 0.6
- **Core total**: $6,000
- **Cap percent**: 30%

### Expected Results
- **Total units**: 5.4
- **Unit cost**: $1,111.11
- **Preliminary shares**: $2,444.44 each
- **Cap amounts**: [$1,350, $960, $840]
- **Result**: All adults capped, deficit warning

## 🚨 Error Handling

### Validation Errors
- Input validation with clear error messages
- Child unit balance checking
- Income and percentage range validation
- Required field enforcement

### Calculation Warnings
- **Deficit after caps**: When income caps prevent reaching Core total
- **Rebalancing limits**: Maximum iteration warnings
- **Vision allocation**: Insufficient funds for sinking funds

### Recovery Options
- Adjust Core total or reclassify items
- Temporarily increase cap percentage
- Set manual overrides
- Revise sinking fund targets

## 🔒 Security & Privacy

### Data Protection
- Input sanitization and validation
- No external data transmission
- Local storage only (development)
- Secure headers with Helmet

### Access Control
- **Admin**: Full household management
- **Adult**: Income, care, voting access
- **ReadOnly**: Reports and documents only

## 🚀 Production Deployment

### Environment Variables
```bash
PORT=3000
NODE_ENV=production
```

### Database Integration
Replace in-memory storage with:
- PostgreSQL for relational data
- Redis for caching
- File storage for documents

### Security Enhancements
- HTTPS enforcement
- Rate limiting
- Authentication system
- Audit logging

## 🤝 Contributing

### Development Setup
1. Fork the repository
2. Create feature branch
3. Make changes with tests
4. Submit pull request

### Code Standards
- ES6+ JavaScript
- JSDoc comments
- Consistent formatting
- Error handling

## 📄 License

MIT License - see LICENSE file for details

## 🆘 Support

### Common Issues
- **Child units don't balance**: Ensure total equals `childrenCount × childUnitWeight`
- **Calculation errors**: Check income values and percentages
- **Import failures**: Validate JSON format and required fields

### Getting Help
- Check validation messages
- Review calculation audit trails
- Export data for debugging
- Check browser console for errors

## 🎉 Success Stories

This system is designed for families who want:
- **Fairness**: Transparent cost sharing based on ability and responsibility
- **Recognition**: Valuing care work and domestic labor
- **Planning**: Long-term financial goals and emergency preparedness
- **Governance**: Structured decision-making and communication

---

**Built with ❤️ for multi-adult families who believe in fair, transparent, and sustainable household finance management.**
