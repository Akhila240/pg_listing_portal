// App.jsx
import { useState } from 'react';
import PropertyCard from './components/PropertyCard';
import FilterBar from './components/FilterBar';
import Pagination from './components/Pagination';
import propertiesData from './data/properties.json';
import './App.css';

const App = () => {
  const [filters, setFilters] = useState({ rent: '', location: '', available: false });
  const [search, setSearch] = useState('');
  const [currentPage, setCurrentPage] = useState(1);
  const itemsPerPage = 5;

  const filteredProperties = propertiesData.filter(property => {
    return (
      (filters.rent === '' || property.rent <= parseInt(filters.rent)) &&
      (filters.location === '' || property.location.toLowerCase().includes(filters.location.toLowerCase())) &&
      (!filters.available || property.available) &&
      (search === '' || property.title.toLowerCase().includes(search.toLowerCase()))
    );
  });

  const paginatedProperties = filteredProperties.slice(
    (currentPage - 1) * itemsPerPage,
    currentPage * itemsPerPage
  );

  return (
    <div className="app">
      <h1>PG Listing Portal</h1>
      <FilterBar filters={filters} setFilters={setFilters} search={search} setSearch={setSearch} />
      <div className="property-list">
        {paginatedProperties.map(property => (
          <PropertyCard key={property.id} property={property} />
        ))}
      </div>
      <Pagination 
        totalItems={filteredProperties.length} 
        itemsPerPage={itemsPerPage} 
        currentPage={currentPage} 
        setCurrentPage={setCurrentPage} 
      />
    </div>
  );
};

export default App;

// components/PropertyCard.jsx
const PropertyCard = ({ property }) => (
  <div className="property-card">
    <img src={property.image} alt={property.title} />
    <h2>{property.title}</h2>
    <p>Rent: ₹{property.rent}</p>
    <p>Location: {property.location}</p>
    <p>{property.available ? 'Available' : 'Not Available'}</p>
  </div>
);

export default PropertyCard;

// components/FilterBar.jsx
const FilterBar = ({ filters, setFilters, search, setSearch }) => {
  const handleChange = e => {
    setFilters({ ...filters, [e.target.name]: e.target.value });
  };

  const handleCheckbox = e => {
    setFilters({ ...filters, available: e.target.checked });
  };

  return (
    <div className="filter-bar">
      <input type="text" name="location" placeholder="Location" value={filters.location} onChange={handleChange} />
      <input type="number" name="rent" placeholder="Max Rent" value={filters.rent} onChange={handleChange} />
      <label>
        <input type="checkbox" checked={filters.available} onChange={handleCheckbox} /> Available only
      </label>
      <input type="text" placeholder="Search title" value={search} onChange={e => setSearch(e.target.value)} />
    </div>
  );
};

export default FilterBar;

// components/Pagination.jsx
const Pagination = ({ totalItems, itemsPerPage, currentPage, setCurrentPage }) => {
  const totalPages = Math.ceil(totalItems / itemsPerPage);

  return (
    <div className="pagination">
      {[...Array(totalPages)].map((_, index) => (
        <button
          key={index}
          className={currentPage === index + 1 ? 'active' : ''}
          onClick={() => setCurrentPage(index + 1)}
        >
          {index + 1}
        </button>
      ))}
    </div>
  );
};

export default Pagination;

// data/properties.json
[
  {
    "id": 1,
    "title": "Spacious PG in Koramangala",
    "rent": 8000,
    "location": "Koramangala",
    "available": true,
    "image": "https://via.placeholder.com/150"
  },
  {
    "id": 2,
    "title": "Affordable PG in Indiranagar",
    "rent": 7000,
    "location": "Indiranagar",
    "available": false,
    "image": "https://via.placeholder.com/150"
  }
  // Add more properties here...
]

// App.css
.app {
  padding: 20px;
  font-family: Arial, sans-serif;
}
.property-list {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
  gap: 1rem;
}
.property-card {
  border: 1px solid #ccc;
  border-radius: 10px;
  padding: 1rem;
  background-color: #f9f9f9;
  text-align: center;
}
.property-card img {
  width: 100%;
  height: 150px;
  object-fit: cover;
  border-radius: 5px;
}
.filter-bar {
  display: flex;
  gap: 10px;
  margin-bottom: 20px;
}
.pagination button {
  margin: 5px;
  padding: 5px 10px;
  border: none;
  border-radius: 5px;
  background: #eee;
  cursor: pointer;
}
.pagination .active {
  background-color: #007bff;
  color: white;
}
