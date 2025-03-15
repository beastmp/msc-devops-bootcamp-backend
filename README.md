# DevOps Bootcamp - Backend

This repository contains the backend application for the DevOps Bootcamp project. The backend provides REST APIs and services that support the frontend application and other system components.

## Features

- RESTful API endpoints for products and orders
- AWS DynamoDB integration for data storage
- AI capabilities with OpenAI Assistant and AWS Bedrock integration
- AWS Lambda function for serverless operations
- Environment configuration via dotenv
- Error handling and validation
- Cross-origin resource sharing (CORS) support

## Technology Stack

- **Runtime**: Node.js with Express
- **Database**: AWS DynamoDB
- **AI Services**: 
  - OpenAI API
  - AWS Bedrock
- **AWS SDK**: AWS SDK for JavaScript
- **Other AWS Services**: Lambda, IAM (Web Identity Tokens)
- **Utilities**: UUID for ID generation
- **Development**: Nodemon for hot reloading
- **Containerization**: Docker (implied by project structure)

## Prerequisites

- Node.js 14+
- npm 6+
- AWS account with appropriate permissions for:
  - DynamoDB
  - Bedrock
  - Lambda
  - IAM
- OpenAI API key
- Git

## Installation and Setup

1. Clone the repository:
   ```
   git clone https://github.com/beastmp/msc-devops-bootcamp-backend.git
   cd msc-devops-bootcamp-backend
   ```

2. Install dependencies:
   ```
   npm install
   ```

3. Set up environment variables:
   - Create a `.env` file in the root directory
   - Add the following variables:
     ```
     PORT=5000
     AWS_REGION=us-east-1
     DYNAMODB_PRODUCTS_TABLE=cloudmart-products
     DYNAMODB_ORDERS_TABLE=cloudmart-orders
     OPENAI_API_KEY=your-openai-api-key
     OPENAI_ASSISTANT_ID=your-openai-assistant-id
     BEDROCK_AGENT_ID=your-bedrock-agent-id
     BEDROCK_AGENT_ALIAS_ID=your-bedrock-agent-alias-id
     ```

4. Start the application:
   ```
   npm start
   ```

   Or for development with auto-reload:
   ```
   npm run dev
   ```

The API should now be running on [http://localhost:5000](http://localhost:5000).

## Available Commands

- `npm start` - Run the application
- `npm run dev` - Run the application with Nodemon for development

## Project Structure

```
src/
├── controllers/           # Request handlers
│   ├── aiController.js    # AI integration controller
│   ├── orderController.js # Order management controller
│   └── productController.js # Product management controller
├── routes/                # API routes
│   ├── aiRoutes.js        # AI endpoints
│   ├── orderRoutes.js     # Order endpoints
│   └── productRoutes.js   # Product endpoints
├── services/              # Business logic
│   ├── aiService.js       # OpenAI and Bedrock integration
│   ├── orderService.js    # Order operations with DynamoDB
│   └── productService.js  # Product operations with DynamoDB
├── lambda/                # AWS Lambda functions
│   └── index.js           # Lambda handler for product recommendations
└── server.js              # Express server configuration and startup
```

## API Endpoints

### Products API
- `GET /api/products` - Get all products
- `GET /api/products/:id` - Get product by ID
- `POST /api/products` - Create a new product
- `PUT /api/products/:id` - Update product
- `DELETE /api/products/:id` - Delete product

### Orders API
- `GET /api/orders` - Get all orders
- `GET /api/orders/:id` - Get order by ID
- `GET /api/orders?email={email}` - Get orders by user email
- `POST /api/orders` - Create a new order
- `PUT /api/orders/:id` - Update order status
- `DELETE /api/orders/:id` - Delete order

### AI API
- `POST /api/ai/openai/conversation` - Start an OpenAI conversation
- `POST /api/ai/openai/message` - Send a message to OpenAI assistant
- `POST /api/ai/bedrock/conversation` - Start an AWS Bedrock conversation
- `POST /api/ai/bedrock/message` - Send a message to AWS Bedrock agent

## Database

The application uses AWS DynamoDB for data storage, with two main tables:
- `cloudmart-products`: Stores product information
- `cloudmart-orders`: Stores order information

### Data Models

#### Product
```javascript
{
  id: String,          // UUID
  name: String,        // Product name
  price: Number,       // Product price
  description: String, // Product description
  image: String,       // Image URL
  createdAt: String    // ISO timestamp
}
```

#### Order
```javascript
{
  id: String,          // UUID
  userEmail: String,   // Customer email
  items: Array,        // Array of ordered products
  status: String,      // Order status (e.g., "Pending", "Shipped", "Delivered", "Canceled")
  createdAt: String    // ISO timestamp
}
```

## AI Integration

This project integrates with both OpenAI's API and AWS Bedrock for AI capabilities:

1. **OpenAI Assistant**: Provides conversational AI with the ability to perform order operations like deletion and cancellation.

2. **AWS Bedrock**: Used for advanced AI features through Amazon's Bedrock Agent service.

## AWS Lambda Function

The project includes a Lambda function that can be deployed to AWS for serverless compute:
- Function: Retrieves product information from DynamoDB
- Trigger: Can be set up with API Gateway or other event sources
- Configuration: Uses environment variables for DynamoDB table name

## Deployment

### Docker

1. Build the Docker image:
   ```
   docker build -t msc-devops-bootcamp-backend .
   ```

2. Run the Docker container:
   ```
   docker run -p 5000:5000 -e AWS_REGION=us-east-1 -e DYNAMODB_PRODUCTS_TABLE=cloudmart-products -e DYNAMODB_ORDERS_TABLE=cloudmart-orders msc-devops-bootcamp-backend
   ```

### AWS Deployment

For AWS deployment instructions including Lambda functions and DynamoDB configuration, see the companion repository: `msc-devops-bootcamp-infrastructure`.

## Kubernetes Deployment

For Kubernetes deployment instructions, see the companion repository: `msc-devops-bootcamp-kubernetes`.

## Contributing

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add some amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## License

This project is licensed under the MIT License - see the LICENSE file for details.

## Contact

Project Link: [https://github.com/beastmp/msc-devops-bootcamp-infrastructure](https://github.com/beastmp/msc-devops-bootcamp-infrastructure)

Project Link: [https://github.com/beastmp/msc-devops-bootcamp-kubernetes](https://github.com/beastmp/msc-devops-bootcamp-kubernetes)

Project Link: [https://github.com/beastmp/msc-devops-bootcamp-frontend](https://github.com/beastmp/msc-devops-bootcamp-frontend)
