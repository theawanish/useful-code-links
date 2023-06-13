# useful-code-links

# https://codesandbox.io/s/recuce-in-javascript-forked-5v7n0



import React, { useState, useEffect, useRef } from 'react';
import Select from 'react-select';

const CustomDropdown = () => {
  const [options, setOptions] = useState([
    { value: 'option1', label: 'Option 1' },
    { value: 'option2', label: 'Option 2' },
    { value: 'option3', label: 'Option 3' },
    { value: 'option4', label: 'Option 4' },
  ]);
  const [selectedOption, setSelectedOption] = useState(null);
  const [searchValue, setSearchValue] = useState('');
  const searchInputRef = useRef(null);

  useEffect(() => {
    // Move the selected option to the top
    if (selectedOption) {
      setOptions((prevOptions) => {
        const filteredOptions = prevOptions.filter(
          (option) => option.value !== selectedOption.value
        );
        return [selectedOption, ...filteredOptions];
      });
    }
  }, [selectedOption]);

  const handleInputChange = (inputValue) => {
    setSearchValue(inputValue);
  };

  const handleChange = (selected) => {
    setSelectedOption(selected);
  };

  const handleClearSearch = () => {
    setSearchValue('');
    searchInputRef.current.focus();
  };

  return (
    <Select
      options={options}
      value={selectedOption}
      onChange={handleChange}
      onInputChange={handleInputChange}
      isSearchable
      inputRef={(ref) => {
        searchInputRef.current = ref;
      }}
      components={{
        Input: (props) => (
          <div>
            <input {...props} />
            {searchValue && (
              <button
                type="button"
                className="clear-icon"
                onClick={handleClearSearch}
              >
                <svg
                  xmlns="http://www.w3.org/2000/svg"
                  viewBox="0 0 24 24"
                  fill="none"
                  stroke="currentColor"
                  strokeWidth="2"
                  strokeLinecap="round"
                  strokeLinejoin="round"
                >
                  <line x1="18" y1="6" x2="6" y2="18" />
                  <line x1="6" y1="6" x2="18" y2="18" />
                </svg>
              </button>
            )}
          </div>
        ),
      }}
    />
  );
};

export default CustomDropdown;
