# Instagram Followers Checker

This Python tool helps you compare your Instagram followers and following lists. It identifies users you follow who do not follow you back and outputs the result to a text file.

## Features

- Log in using Instagram session for secure access.
- Fetches your followers and following lists.
- Compares the two lists to find users who don't follow you back.
- Outputs the results to a specified text file.

## Requirements

- Python 3.10.X+
- `Instaloader` Python package

## Installation

1. Clone the repository or download the files:

    ```bash
    git clone https://github.com/xl-spooky/instagram-tool.git
    cd instagram-tool
    ```

2. Install the required dependencies:

    ```bash
    pip install instaloader
    ```

## Usage

### Step 1: Create a Session File

First, you need to create a session file for your Instagram account. This will allow the tool to access your Instagram data securely without repeatedly asking for your password.

Run the following command to generate a session file:

```bash
instaloader --login your_instagram_username --sessionfile=session-your_instagram_username
```

- Replace `your_instagram_username` with your actual Instagram username.
- After entering your password and completing any two-factor authentication (if enabled), a session file named `session-your_instagram_username` will be created in the current directory.

### Step 2: Edit the Script to Use Your Session File

Open the `main.py` script and edit the following line:

```python
loader.load_session_from_file(username, filename="session-username")
```

Replace `session-username` with the session file you generated in Step 1. For example, if your session file is `session-johndoe`, change it to:

```python
loader.load_session_from_file(username, filename="session-johndoe")
```

### Step 3: Run the Script

Now you can run the script to compare your followers and following lists. Use the following command:

```bash
python main.py --username your_instagram_username --output non_followers.txt
```

- Replace `your_instagram_username` with your actual Instagram username.
- The `--output` argument specifies the file where the list of users who don't follow you back will be saved. The default file name is `non_followers.txt`, but you can specify any file name.

### Example

```bash
python main.py --username johndoe --output unfollowers.txt
```

This will save the results in a file named `unfollowers.txt`.

### Step 4: Check the Output

Once the script completes, open the output file to see the list of users who don't follow you back:

```bash
cat non_followers.txt
```

### Notes

- **Rate Limits**: Instagram imposes rate limits on API requests. If you see a `401 Unauthorized` error or a message like "Please wait a few minutes before you try again," wait for 10-15 minutes and try running the script again.
- **Delay Between Requests**: To avoid hitting Instagram’s rate limits, the script includes a 60-second delay between requests. You can adjust this if needed, but be mindful of Instagram’s rate-limiting policies.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Contributing

If you'd like to contribute to this project, feel free to submit a pull request. Please ensure that your code follows the established style and passes all tests.

---

### Troubleshooting

1. **401 Unauthorized Errors**:
    - If you encounter a `401 Unauthorized` error or a "Please wait a few minutes before you try again" message, this means that Instagram has temporarily blocked your requests due to hitting their rate limits. The script automatically includes a delay to reduce this, but if it persists, simply wait a few minutes and try again.

2. **Session File Issues**:
    - If the session file is not found, ensure you’ve generated it correctly using the `instaloader --login` command. If you generate the session file in a different directory, make sure to update the path in the script.
