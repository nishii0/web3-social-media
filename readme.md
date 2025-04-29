// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

contract Web3Social {
    struct Post {
        uint id;
        address author;
        string content;
        uint timestamp;
    }

    uint public postCount = 0;
    mapping(uint => Post) public posts;

    event PostCreated(uint id, address indexed author, string content, uint timestamp);

    // Create a new post
    function createPost(string calldata _content) external {
        require(bytes(_content).length > 0, "Content cannot be empty");

        postCount++;
        posts[postCount] = Post(postCount, msg.sender, _content, block.timestamp);
        emit PostCreated(postCount, msg.sender, _content, block.timestamp);
    }

    // Retrieve a post by ID
    function getPost(uint _id) external view returns (Post memory) {
        require(_id > 0 && _id <= postCount, "Post does not exist");
        return posts[_id];
    }
}
