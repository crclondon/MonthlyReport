import React, { useState, useEffect } from 'react';
import { Search, ChevronDown, Download, Lock, Eye, EyeOff } from 'lucide-react';

const SimpleAuthDashboard = () => {
  const [isAuthenticated, setIsAuthenticated] = useState(false);
  const [password, setPassword] = useState('');
  const [showPassword, setShowPassword] = useState(false);
  const [error, setError] = useState('');
  
  // 🔐 SUPER SIMPLE: Just one password! Change this to whatever you want.
  const CORRECT_PASSWORD = 'CRC2025';

  const [searchTerm, setSearchTerm] = useState('');
  const [campusFilter, setCampusFilter] = useState('All');

  // Your actual data from the CSV
  const dashboardData = [
    { campus: 'Ashford', zonePastor: 'Ps Eddie Coetzee (ZP)', internPastor: 'Ps Eddie Coetzee (IP)', overseer: 'Ps Eddie Coetzee (OV)', supervisor: '', homecellLeaders: 'Ps Eddie Coetzee Prodigals', salvations: 0, ftv: 0, attAdult: '0%', attChild: '0%', adultSigned: 0, totalAdult: 9, totalChild: 3, goalSal: '0%', goalFtv: '0%', goalAtt: '0%' },
    { campus: 'Ashford', zonePastor: 'Ps Eddie Coetzee (ZP)', internPastor: 'Ps Eddie Coetzee (IP)', overseer: 'Ps Eddie Coetzee (OV)', supervisor: 'Ps Eddie Coetzee (ZS)', homecellLeaders: 'Clive Madden', salvations: 0, ftv: 1, attAdult: '24%', attChild: 'N/A', adultSigned: 0, totalAdult: 6, totalChild: 0, goalSal: '0%', goalFtv: '25%', goalAtt: '35%' },
    { campus: 'Ashford', zonePastor: 'Ps Eddie Coetzee (ZP)', internPastor: 'Ps Eddie Coetzee (IP)', overseer: 'Ps Eddie Coetzee (OV)', supervisor: 'Ps Eddie Coetzee (ZS)', homecellLeaders: 'Holly Ballan', salvations: 0, ftv: 0, attAdult: '49%', attChild: '80%', adultSigned: 0, totalAdult: 4, totalChild: 4, goalSal: '0%', goalFtv: '0%', goalAtt: '70%' },
    { campus: 'Ashford', zonePastor: 'Ps Eddie Coetzee (ZP)', internPastor: 'Ps Eddie Coetzee (IP)', overseer: 'Ps Eddie Coetzee (OV)', supervisor: 'Ps Eddie Coetzee (ZS)', homecellLeaders: 'Ps Eddie Coetzee Leaders', salvations: 0, ftv: 1, attAdult: '80%', attChild: '60%', adultSigned: 0, totalAdult: 2, totalChild: 1, goalSal: '0%', goalFtv: '25%', goalAtt: '114%' },
    { campus: 'Ashford', zonePastor: 'Ps Eddie Coetzee (ZP)', internPastor: 'Ps Eddie Coetzee (IP)', overseer: 'Ps Eddie Coetzee (OV)', supervisor: 'Ps Eddie Coetzee (ZS)', homecellLeaders: 'Zigi Ballan', salvations: 1, ftv: 0, attAdult: '28%', attChild: '50%', adultSigned: 0, totalAdult: 10, totalChild: 8, goalSal: '100%', goalFtv: '0%', goalAtt: '40%' },
    { campus: 'East Barnet', zonePastor: 'Ps Kester Olarewaju (ZP)', internPastor: 'Ps Kester Olarewaju (IP)', overseer: '', supervisor: '', homecellLeaders: 'Ps Kester Olarewaju Leaders', salvations: 2, ftv: 3, attAdult: '28%', attChild: '0%', adultSigned: 0, totalAdult: 4, totalChild: 3, goalSal: '200%', goalFtv: '75%', goalAtt: '39%' },
    { campus: 'East Barnet', zonePastor: 'Ps Kester Olarewaju (ZP)', internPastor: 'Ps Kester Olarewaju (IP)', overseer: '', supervisor: '', homecellLeaders: 'Ps Kester Olarewaju Prodigals', salvations: 0, ftv: 0, attAdult: '0%', attChild: '0%', adultSigned: 0, totalAdult: 131, totalChild: 27, goalSal: '0%', goalFtv: '0%', goalAtt: '0%' },
    { campus: 'East Barnet', zonePastor: 'Ps Kester Olarewaju (ZP)', internPastor: 'Ps Kester Olarewaju (IP)', overseer: 'Kaylene Thaver (OV)', supervisor: 'Kaylene Thaver (ZS)', homecellLeaders: 'James Jarvis', salvations: 1, ftv: 6, attAdult: '14%', attChild: 'N/A', adultSigned: 0, totalAdult: 9, totalChild: 0, goalSal: '100%', goalFtv: '150%', goalAtt: '21%' },
    { campus: 'East Barnet', zonePastor: 'Ps Kester Olarewaju (ZP)', internPastor: 'Ps Kester Olarewaju (IP)', overseer: 'Kaylene Thaver (OV)', supervisor: 'Kaylene Thaver (ZS)', homecellLeaders: 'Marlize Bothma', salvations: 2, ftv: 5, attAdult: '13%', attChild: '27%', adultSigned: 0, totalAdult: 11, totalChild: 9, goalSal: '200%', goalFtv: '125%', goalAtt: '18%' },
    { campus: 'East Barnet', zonePastor: 'Ps Kester Olarewaju (ZP)', internPastor: 'Ps Kester Olarewaju (IP)', overseer: 'Kaylene Thaver (OV)', supervisor: 'Kaylene Thaver (ZS)', homecellLeaders: 'Noreen Magomo', salvations: 0, ftv: 2, attAdult: '27%', attChild: '0%', adultSigned: 0, totalAdult: 11, totalChild: 3, goalSal: '0%', goalFtv: '50%', goalAtt: '38%' },
    { campus: 'East Barnet', zonePastor: 'Ps Kester Olarewaju (ZP)', internPastor: 'Ps Kester Olarewaju (IP)', overseer: 'Ps Anton Snyman (OV)', supervisor: 'Linette Snyman (ZS)', homecellLeaders: 'Linette Snyman', salvations: 0, ftv: 0, attAdult: '38%', attChild: '48%', adultSigned: 0, totalAdult: 14, totalChild: 8, goalSal: '0%', goalFtv: '0%', goalAtt: '55%' },
    { campus: 'East Barnet', zonePastor: 'Ps Kester Olarewaju (ZP)', internPastor: 'Ps Kester Olarewaju (IP)', overseer: 'Ps Anton Snyman (OV)', supervisor: 'Linette Snyman (ZS)', homecellLeaders: 'Rima Kubiliene', salvations: 0, ftv: 1, attAdult: '30%', attChild: '60%', adultSigned: 0, totalAdult: 5, totalChild: 1, goalSal: '0%', goalFtv: '25%', goalAtt: '43%' },
    { campus: 'East Barnet', zonePastor: 'Ps Kester Olarewaju (ZP)', internPastor: 'Ps Kester Olarewaju (IP)', overseer: 'Ps Anton Snyman (OV)', supervisor: 'Ps Anton Snyman (ZS)', homecellLeaders: 'Ps Anton Snyman', salvations: 1, ftv: 1, attAdult: '10%', attChild: '0%', adultSigned: 0, totalAdult: 10, totalChild: 1, goalSal: '100%', goalFtv: '25%', goalAtt: '14%' },
    { campus: 'East Barnet', zonePastor: 'Ps Kester Olarewaju (ZP)', internPastor: 'Ps Kester Olarewaju (IP)', overseer: 'Ps Anton Snyman (OV)', supervisor: 'Ps Anton Snyman (ZS)', homecellLeaders: 'Sesitwa Mohlala', salvations: 5, ftv: 5, attAdult: '30%', attChild: '0%', adultSigned: 0, totalAdult: 6, totalChild: 2, goalSal: '500%', goalFtv: '125%', goalAtt: '43%' },
    { campus: 'East Barnet', zonePastor: 'Ps Kester Olarewaju (ZP)', internPastor: 'Ps Kester Olarewaju (IP)', overseer: 'Ps Anton Snyman (OV)', supervisor: 'Ps Anton Snyman (ZS)', homecellLeaders: 'Tinus Moolman', salvations: 1, ftv: 1, attAdult: '49%', attChild: 'N/A', adultSigned: 0, totalAdult: 5, totalChild: 0, goalSal: '100%', goalFtv: '25%', goalAtt: '70%' },
    { campus: 'East Barnet', zonePastor: 'Ps Kester Olarewaju (ZP)', internPastor: '', overseer: '', supervisor: '', homecellLeaders: 'Victor Bolaji Ode', salvations: 0, ftv: 0, attAdult: '50%', attChild: 'N/A', adultSigned: 0, totalAdult: 3, totalChild: 0, goalSal: '0%', goalFtv: '0%', goalAtt: '71%' },
    { campus: 'East Barnet', zonePastor: 'Ps Kester Olarewaju (ZP)', internPastor: '', overseer: '', supervisor: '', homecellLeaders: 'Benjamin Jean-Jacques III', salvations: 3, ftv: 5, attAdult: '38%', attChild: '0%', adultSigned: 0, totalAdult: 10, totalChild: 1, goalSal: '300%', goalFtv: '125%', goalAtt: '54%' },
    { campus: 'East Barnet', zonePastor: 'Ps Kester Olarewaju (ZP)', internPastor: '', overseer: '', supervisor: '', homecellLeaders: 'Divine Egbedi', salvations: 0, ftv: 2, attAdult: '36%', attChild: 'N/A', adultSigned: 0, totalAdult: 6, totalChild: 0, goalSal: '0%', goalFtv: '50%', goalAtt: '51%' },
    { campus: 'East Barnet', zonePastor: 'Ps Kester Olarewaju (ZP)', internPastor: '', overseer: '', supervisor: '', homecellLeaders: 'Hannah Shewan', salvations: 0, ftv: 0, attAdult: '21%', attChild: 'N/A', adultSigned: 0, totalAdult: 9, totalChild: 0, goalSal: '0%', goalFtv: '0%', goalAtt: '30%' },
    { campus: 'East Barnet', zonePastor: 'Ps Kester Olarewaju (ZP)', internPastor: '', overseer: '', supervisor: '', homecellLeaders: 'Larisa Spring', salvations: 0, ftv: 0, attAdult: '0%', attChild: '0%', adultSigned: 0, totalAdult: 9, totalChild: 3, goalSal: '0%', goalFtv: '0%', goalAtt: '0%' },
    { campus: 'East Barnet', zonePastor: 'Ps Kester Olarewaju (ZP)', internPastor: '', overseer: '', supervisor: '', homecellLeaders: 'Maria Olarewaju', salvations: 1, ftv: 3, attAdult: '53%', attChild: 'N/A', adultSigned: 0, totalAdult: 3, totalChild: 0, goalSal: '100%', goalFtv: '75%', goalAtt: '76%' },
    { campus: 'East Barnet', zonePastor: 'Ps Kester Olarewaju (ZP)', internPastor: '', overseer: '', supervisor: '', homecellLeaders: 'Nadine Lewis', salvations: 0, ftv: 2, attAdult: '45%', attChild: '73%', adultSigned: 0, totalAdult: 4, totalChild: 3, goalSal: '0%', goalFtv: '50%', goalAtt: '64%' },
    { campus: 'East Barnet', zonePastor: 'Ps Kester Olarewaju (ZP)', internPastor: '', overseer: '', supervisor: '', homecellLeaders: 'Felicia Tchen Belfast', salvations: 0, ftv: 0, attAdult: '10%', attChild: 'N/A', adultSigned: 0, totalAdult: 3, totalChild: 0, goalSal: '0%', goalFtv: '0%', goalAtt: '14%' },
  ];

  const [filteredData, setFilteredData] = useState(dashboardData);

  useEffect(() => {
    const storedAuth = sessionStorage.getItem('churchAuth');
    if (storedAuth === 'true') {
      setIsAuthenticated(true);
    }
  }, []);

  useEffect(() => {
    let filtered = dashboardData;

    if (campusFilter !== 'All') {
      filtered = filtered.filter(row => row.campus === campusFilter);
    }

    if (searchTerm) {
      filtered = filtered.filter(row =>
        row.homecellLeaders.toLowerCase().includes(searchTerm.toLowerCase()) ||
        row.campus.toLowerCase().includes(searchTerm.toLowerCase())
      );
    }

    setFilteredData(filtered);
  }, [campusFilter, searchTerm]);

  const handleLogin = (e) => {
    e.preventDefault();
    if (password === CORRECT_PASSWORD) {
      setIsAuthenticated(true);
      sessionStorage.setItem('churchAuth', 'true');
    } else {
      setError('Incorrect password');
      setPassword('');
    }
  };

  const handleLogout = () => {
    setIsAuthenticated(false);
    sessionStorage.removeItem('churchAuth');
  };

  const getColor = (value, type) => {
    if (!value || value === 'N/A' || value === '0%') return 'white';
    const num = parseInt(value);
    if (type === 'attendance') {
      if (num >= 70) return '#90EE90';
      if (num >= 40) return '#FFD580';
      return '#FFB6C1';
    }
    if (type === 'goal') {
      if (num >= 100) return '#90EE90';
      if (num >= 50) return '#FFD580';
      return '#FFB6C1';
    }
    return 'white';
  };

  // Login Screen
  if (!isAuthenticated) {
    return (
      <div style={{
        minHeight: '100vh',
        display: 'flex',
        alignItems: 'center',
        justifyContent: 'center',
        background: 'linear-gradient(135deg, #1e3a8a 0%, #3b82f6 100%)',
        fontFamily: "'Segoe UI', Tahoma, Geneva, Verdana, sans-serif"
      }}>
        <div style={{
          backgroundColor: 'white',
          padding: '50px 40px',
          borderRadius: '16px',
          boxShadow: '0 20px 60px rgba(0,0,0,0.3)',
          width: '100%',
          maxWidth: '450px'
        }}>
          <div style={{
            display: 'flex',
            flexDirection: 'column',
            alignItems: 'center',
            marginBottom: '35px'
          }}>
            <div style={{
              backgroundColor: '#1e3a8a',
              borderRadius: '16px',
              padding: '20px',
              marginBottom: '20px'
            }}>
              <Lock size={40} color="white" />
            </div>
            <h1 style={{
              margin: '0 0 10px 0',
              fontSize: '28px',
              fontWeight: '700',
              color: '#1e293b'
            }}>
              CRC London
            </h1>
            <p style={{
              color: '#64748b',
              margin: 0,
              fontSize: '15px'
            }}>
              Monthly Homecell Report
            </p>
          </div>

          <form onSubmit={handleLogin}>
            <div style={{ marginBottom: '25px', position: 'relative' }}>
              <label style={{
                display: 'block',
                marginBottom: '10px',
                fontSize: '14px',
                fontWeight: '600',
                color: '#334155'
              }}>
                Password
              </label>
              <div style={{ position: 'relative' }}>
                <input
                  type={showPassword ? 'text' : 'password'}
                  value={password}
                  onChange={(e) => setPassword(e.target.value)}
                  placeholder="Enter password"
                  required
                  autoFocus
                  style={{
                    width: '100%',
                    padding: '14px 45px 14px 16px',
                    border: error ? '2px solid #ef4444' : '2px solid #e2e8f0',
                    borderRadius: '10px',
                    fontSize: '15px',
                    outline: 'none',
                    boxSizing: 'border-box'
                  }}
                />
                <button
                  type="button"
                  onClick={() => setShowPassword(!showPassword)}
                  style={{
                    position: 'absolute',
                    right: '12px',
                    top: '50%',
                    transform: 'translateY(-50%)',
                    background: 'none',
                    border: 'none',
                    cursor: 'pointer',
                    color: '#64748b'
                  }}
                >
                  {showPassword ? <EyeOff size={20} /> : <Eye size={20} />}
                </button>
              </div>
            </div>

            {error && (
              <div style={{
                backgroundColor: '#fee2e2',
                color: '#991b1b',
                padding: '14px',
                borderRadius: '10px',
                marginBottom: '20px',
                fontSize: '14px'
              }}>
                {error}
              </div>
            )}

            <button
              type="submit"
              style={{
                width: '100%',
                padding: '16px',
                backgroundColor: '#1e3a8a',
                color: 'white',
                border: 'none',
                borderRadius: '10px',
                fontSize: '16px',
                fontWeight: '600',
                cursor: 'pointer'
              }}
            >
              Access Dashboard
            </button>
          </form>
        </div>
      </div>
    );
  }

  // Dashboard
  const uniqueCampuses = ['All', ...new Set(dashboardData.map(row => row.campus))];

  return (
    <div style={{ 
      fontFamily: "'Segoe UI', Tahoma, Geneva, Verdana, sans-serif",
      padding: '20px',
      backgroundColor: '#f5f5f5',
      minHeight: '100vh'
    }}>
      {/* Header */}
      <div style={{
        background: 'linear-gradient(135deg, #1e3a8a 0%, #3b82f6 100%)',
        padding: '30px',
        borderRadius: '12px',
        marginBottom: '20px',
        display: 'flex',
        justifyContent: 'space-between',
        alignItems: 'center',
        flexWrap: 'wrap'
      }}>
        <div>
          <h1 style={{
            color: 'white',
            margin: '0 0 10px 0',
            fontSize: '32px',
            fontWeight: '700'
          }}>
            November - Church Report
          </h1>
          <p style={{
            color: 'rgba(255,255,255,0.9)',
            margin: 0
          }}>
            CRC London - Homecell Performance
          </p>
        </div>
        <button
          onClick={handleLogout}
          style={{
            padding: '12px 24px',
            backgroundColor: 'rgba(255,255,255,0.2)',
            color: 'white',
            border: '2px solid rgba(255,255,255,0.3)',
            borderRadius: '8px',
            cursor: 'pointer'
          }}
        >
          Logout
        </button>
      </div>

      {/* Filters */}
      <div style={{
        backgroundColor: 'white',
        padding: '20px',
        borderRadius: '12px',
        marginBottom: '20px',
        display: 'flex',
        gap: '15px',
        flexWrap: 'wrap'
      }}>
        <div style={{ flex: '1 1 300px', position: 'relative' }}>
          <Search style={{
            position: 'absolute',
            left: '12px',
            top: '50%',
            transform: 'translateY(-50%)',
            color: '#94a3b8'
          }} />
          <input
            type="text"
            placeholder="Search..."
            value={searchTerm}
            onChange={(e) => setSearchTerm(e.target.value)}
            style={{
              width: '100%',
              padding: '12px 12px 12px 40px',
              border: '2px solid #e2e8f0',
              borderRadius: '8px',
              boxSizing: 'border-box'
            }}
          />
        </div>

        <select
          value={campusFilter}
          onChange={(e) => setCampusFilter(e.target.value)}
          style={{
            padding: '12px',
            border: '2px solid #e2e8f0',
            borderRadius: '8px',
            minWidth: '200px'
          }}
        >
          {uniqueCampuses.map(campus => (
            <option key={campus} value={campus}>{campus}</option>
          ))}
        </select>
      </div>

      {/* Stats */}
      <div style={{
        display: 'grid',
        gridTemplateColumns: 'repeat(auto-fit, minmax(200px, 1fr))',
        gap: '15px',
        marginBottom: '20px'
      }}>
        <div style={{
          backgroundColor: 'white',
          padding: '20px',
          borderRadius: '12px',
          borderLeft: '4px solid #3b82f6'
        }}>
          <div style={{ color: '#64748b', fontSize: '14px' }}>Homecells</div>
          <div style={{ fontSize: '32px', fontWeight: '700' }}>
            {filteredData.length}
          </div>
        </div>
        <div style={{
          backgroundColor: 'white',
          padding: '20px',
          borderRadius: '12px',
          borderLeft: '4px solid #10b981'
        }}>
          <div style={{ color: '#64748b', fontSize: '14px' }}>Salvations</div>
          <div style={{ fontSize: '32px', fontWeight: '700' }}>
            {filteredData.reduce((sum, row) => sum + row.salvations, 0)}
          </div>
        </div>
        <div style={{
          backgroundColor: 'white',
          padding: '20px',
          borderRadius: '12px',
          borderLeft: '4px solid #f59e0b'
        }}>
          <div style={{ color: '#64748b', fontSize: '14px' }}>Visitors</div>
          <div style={{ fontSize: '32px', fontWeight: '700' }}>
            {filteredData.reduce((sum, row) => sum + row.ftv, 0)}
          </div>
        </div>
        <div style={{
          backgroundColor: 'white',
          padding: '20px',
          borderRadius: '12px',
          borderLeft: '4px solid #8b5cf6'
        }}>
          <div style={{ color: '#64748b', fontSize: '14px' }}>Members</div>
          <div style={{ fontSize: '32px', fontWeight: '700' }}>
            {filteredData.reduce((sum, row) => sum + row.totalAdult + row.totalChild, 0)}
          </div>
        </div>
      </div>

      {/* Table */}
      <div style={{
        backgroundColor: 'white',
        borderRadius: '12px',
        overflow: 'hidden'
      }}>
        <div style={{ overflowX: 'auto' }}>
          <table style={{
            width: '100%',
            borderCollapse: 'collapse',
            fontSize: '12px'
          }}>
            <thead>
              <tr style={{ backgroundColor: '#1e3a8a', color: 'white' }}>
                <th style={{ padding: '12px', textAlign: 'left' }}>Campus</th>
                <th style={{ padding: '12px', textAlign: 'left' }}>Homecell Leaders</th>
                <th style={{ padding: '12px', textAlign: 'center' }}>SAL</th>
                <th style={{ padding: '12px', textAlign: 'center' }}>FTV</th>
                <th style={{ padding: '12px', textAlign: 'center' }}>ATT Adult</th>
                <th style={{ padding: '12px', textAlign: 'center' }}>ATT Child</th>
                <th style={{ padding: '12px', textAlign: 'center' }}>Adult</th>
                <th style={{ padding: '12px', textAlign: 'center' }}>Child</th>
                <th style={{ padding: '12px', textAlign: 'center' }}>Goal SAL</th>
                <th style={{ padding: '12px', textAlign: 'center' }}>Goal FTV</th>
                <th style={{ padding: '12px', textAlign: 'center' }}>Goal ATT</th>
              </tr>
            </thead>
            <tbody>
              {filteredData.map((row, index) => (
                <tr key={index} style={{
                  backgroundColor: index % 2 === 0 ? '#f8fafc' : 'white'
                }}>
                  <td style={{ padding: '10px', fontWeight: '600' }}>{row.campus}</td>
                  <td style={{ padding: '10px' }}>{row.homecellLeaders}</td>
                  <td style={{ padding: '10px', textAlign: 'center', backgroundColor: row.salvations > 0 ? '#90EE90' : 'white', fontWeight: '600' }}>{row.salvations}</td>
                  <td style={{ padding: '10px', textAlign: 'center', backgroundColor: row.ftv > 0 ? '#90EE90' : 'white', fontWeight: '600' }}>{row.ftv}</td>
                  <td style={{ padding: '10px', textAlign: 'center', backgroundColor: getColor(row.attAdult, 'attendance'), fontWeight: '600' }}>{row.attAdult}</td>
                  <td style={{ padding: '10px', textAlign: 'center', backgroundColor: row.attChild !== 'N/A' ? getColor(row.attChild, 'attendance') : 'white', fontWeight: '600' }}>{row.attChild}</td>
                  <td style={{ padding: '10px', textAlign: 'center', fontWeight: '600' }}>{row.totalAdult}</td>
                  <td style={{ padding: '10px', textAlign: 'center', fontWeight: '600' }}>{row.totalChild}</td>
                  <td style={{ padding: '10px', textAlign: 'center', backgroundColor: getColor(row.goalSal, 'goal'), fontWeight: '600' }}>{row.goalSal}</td>
                  <td style={{ padding: '10px', textAlign: 'center', backgroundColor: getColor(row.goalFtv, 'goal'), fontWeight: '600' }}>{row.goalFtv}</td>
                  <td style={{ padding: '10px', textAlign: 'center', backgroundColor: getColor(row.goalAtt, 'goal'), fontWeight: '600' }}>{row.goalAtt}</td>
                </tr>
              ))}
            </tbody>
          </table>
        </div>
      </div>

      {/* Legend */}
      <div style={{
        marginTop: '20px',
        padding: '20px',
        backgroundColor: 'white',
        borderRadius: '12px'
      }}>
        <h3 style={{ margin: '0 0 15px 0', fontSize: '16px' }}>Color Legend</h3>
        <div style={{ display: 'flex', gap: '30px', flexWrap: 'wrap' }}>
          <div style={{ display: 'flex', alignItems: 'center', gap: '10px' }}>
            <div style={{ width: '24px', height: '24px', backgroundColor: '#90EE90', borderRadius: '4px' }}></div>
            <span>Excellent (≥70% or ≥100%)</span>
          </div>
          <div style={{ display: 'flex', alignItems: 'center', gap: '10px' }}>
            <div style={{ width: '24px', height: '24px', backgroundColor: '#FFD580', borderRadius: '4px' }}></div>
            <span>Good (40-69% or 50-99%)</span>
          </div>
          <div style={{ display: 'flex', alignItems: 'center', gap: '10px' }}>
            <div style={{ width: '24px', height: '24px', backgroundColor: '#FFB6C1', borderRadius: '4px' }}></div>
            <span>Needs Attention (&lt;40% or &lt;50%)</span>
          </div>
        </div>
      </div>
    </div>
  );
};

export default SimpleAuthDashboard;
