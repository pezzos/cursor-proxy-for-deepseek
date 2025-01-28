# Cursor Deepseek API Proxy

This project sets up a Docker Compose configuration for the Cursor Deepseek API Proxy, which was not originally provided in the [danilofalcao/cursor-deepseek](https://github.com/danilofalcao/cursor-deepseek) repository. This setup specifically uses the Deepseek Coder model, which is optimized for code-related tasks.

## How It Works

1. **Docker Compose Setup**: The `docker-compose.yml` file defines the service `cursor-deepseek` which builds the Docker image and runs the proxy.
2. **Environment Variables**: The `.env` file contains necessary environment variables such as `DEEPSEEK_API_KEY` and network configurations.
3. **Traefik Integration**: The service is integrated with Traefik for HTTPS routing and load balancing.

## Prerequisites
Make sure you have the following prerequisites installed on your machine:

- Docker with Docker Compose
- Traefik (configured as your reverse proxy)
- Cursor IDE

## Why you need Traefik for Cursor

Traefik is essential in this setup for several reasons:

1. **Secure Access**: Traefik provides HTTPS termination, ensuring that all communications between Cursor and your Ollama instance are encrypted.
2. **Domain Routing**: It allows you to expose Ollama through a custom domain, which is required for Cursor integration as the LLM should be accessible from the Cursor servers.
3. **Authentication**: Traefik can handle authentication layers, adding security to your LLM endpoint.
4. **Load Balancing**: If you scale your Ollama instances, Traefik can distribute the load effectively.

Without Traefik, you would need to manually configure SSL certificates and routing, which can be complex and error-prone.

## Getting Started

1. Clone this repository:
    ```bash
    git clone https://github.com/pezzos/docker-config-deepseek_api_proxy.git
    ```
2. Change to the project directory:
    ```bash
    cd docker-config-deepseek_api_proxy
    ```
3. Configure your domain in the `.env` file from the `.env.example`, and change it accordingly, especially:
    ```bash
    DOMAIN=your-domain.com # To point to the domain handled by your Treafik
    DEEPSEEK_API_KEY=sk-1234 # To push your key to DeepSeek
    ```
4. Run `docker-compose up -d` to start the service.

## Exposing the API in Cursor

To use this API in Cursor, you need to configure the URL generated by Traefik. The URL will be in the format `https://cursor-deepseek.yourdomain.com/v1`. Make sure to append `/v1` to the URL when configuring it in Cursor. Additionally, in Cursor, you should select `gpt-4o` as the model to ensure compatibility with the API.

### Then in Cursor:

1. Open Cursor settings
2. In the AI models section:
   - Use `gpt-4o` as Cursor constrains the list of usable model for the Composer
   - Disable other models to ensure you're using the right one
3. In the OpenAI configuration:
   - Paste your Deepseek API key
   - Add the API URL: https://cursor-deepseek.yourdomain.com/v1
4. Test the connection by trying a simple prompt like "Write a hello world in Python"

## Stop and Cleanup

To stop the containers and remove the network:
```bash
docker-compose down
```

To completely remove all data (including models):
```bash
docker-compose down -v
```

## Acknowledgments

This setup is based on the original work from [danilofalcao/cursor-deepseek](https://github.com/danilofalcao/cursor-deepseek).

## Contributing

We welcome contributions! If you'd like to contribute to the Ollama Docker Traefik Setup:

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Submit a pull request

Please ensure your code follows our coding standards and includes appropriate documentation.

## License

This project is licensed under the [MIT License](LICENSE). Feel free to use, modify, and distribute it according to the terms of the license. We appreciate attribution and mentions in derivative works.

## Support

If you encounter any issues or have questions:
1. Check the existing issues on GitHub
2. Create a new issue with detailed information about your problem
3. Join our community discussions
