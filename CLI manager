 const fs = require('fs');
const path = require('path');
const readline = require('readline');

const rl = readline.createInterface({
  input: process.stdin,
  output: process.stdout
});

const commands = {
  list: (dir = '.') => {
    fs.readdir(dir, (err, files) => {
      if (err) {
        console.error('Error reading directory:', err.message);
        return;
      }
      console.log('Files:', files.join(', '));
    });
  },

  read: (file) => {
    if (!file) {
      console.error('Please provide a file name.');
      return;
    }
    fs.readFile(file, 'utf8', (err, data) => {
      if (err) {
        console.error('Error reading file:', err.message);
        return;
      }
      console.log(data);
    });
  },

  create: (file, ...content) => {
    if (!file) {
      console.error('Please provide a file name.');
      return;
    }
    fs.writeFile(file, content.join(' '), (err) => {
      if (err) {
        console.error('Error creating file:', err.message);
        return;
      }
      console.log(`${file} created successfully.`);
    });
  },

  delete: (file) => {
    if (!file) {
      console.error('Please provide a file name.');
      return;
    }
    fs.unlink(file, (err) => {
      if (err) {
        console.error('Error deleting file:', err.message);
        return;
      }
      console.log(`${file} deleted successfully.`);
    });
  },

  exit: () => {
    console.log('Exiting CLI file manager.');
    rl.close();
    process.exit(0);
  }
};

const prompt = () => {
  rl.question('Enter command: ', (input) => {
    const [cmd, ...args] = input.trim().split(' ');
    if (commands[cmd]) {
      commands[cmd](...args);
    } else {
      console.log('Unknown command');
    }
    prompt();
  });
};

console.log('CLI File Manager started. Available commands: list, read <file>, create <file> <content>, delete <file>, exit');
prompt();
